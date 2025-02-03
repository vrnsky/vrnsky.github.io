---
title: Spring Boot interaction with Kafka with HTTPS
type: blog
sidebar:
  open: true
date: 2023-01-22
comments: true
---

In this article, we will be developing a Spring Boot application that works with Kafka and terminates traffic via HTTPS.
So first of all we have to generate self-signed certificates by following the bash script.

```bash
#!/bin/bash

set -o nounset \
-o errexit \
-o verbose \
-o xtrace

# Generate CA key
openssl req -new -x509 -keyout snakeoil-ca-1.key -out snakeoil-ca-1.crt -days 365 -subj ‘/CN=localhost/OU=TEST/O=MEDIUM/L=PaloAlto/S=Ca/C=US’ -passin pass:medium -passout pass:medium
# openssl req -new -x509 -keyout snakeoil-ca-2.key -out snakeoil-ca-2.crt -days 365 -subj ‘/CN=ca2.test.confluent.io/OU=TEST/O=MEDIUM/L=PaloAlto/S=Ca/C=US’ -passin pass:meduim -passout pass:medium

# Kafkacat
openssl genrsa -des3 -passout “pass:medmium” -out kafkacat.client.key 1024
openssl req -passin “pass:medium” -passout “pass:medium” -key kafkacat.client.key -new -out kafkacat.client.req -subj ‘/CN=localhost/OU=TEST/O=MEDIUM/L=PaloAlto/S=Ca/C=US’
openssl x509 -req -CA snakeoil-ca-1.crt -CAkey snakeoil-ca-1.key -in kafkacat.client.req -out kafkacat-ca1-signed.pem -days 9999 -CAcreateserial -passin “pass:medium”


for i in broker1 consumer # we are going to generate certs for broker(zookeper) and cosumer(our app)
do
echo $i
# Create keystores
keytool -genkey -noprompt \
-alias $i \
-dname “CN=localhost, OU=TEST, O=MEDIUM, L=PaloAlto, S=Ca, C=US” \
-keystore kafka.$i.keystore.jks \
-keyalg RSA \
-storepass confluent \
-keypass confluent

# Create CSR, sign the key and import back into keystore
keytool -keystore kafka.$i.keystore.jks -alias $i -certreq -file $i.csr -storepass confluent -keypass medium

openssl x509 -req -CA snakeoil-ca-1.crt -CAkey snakeoil-ca-1.key -in $i.csr -out $i-ca1-signed.crt -days 9999 -CAcreateserial -passin pass:medium

keytool -keystore kafka.$i.keystore.jks -alias CARoot -import -file snakeoil-ca-1.crt -storepass meduim -keypass medium

keytool -keystore kafka.$i.keystore.jks -alias $i -import -file $i-ca1-signed.crt -storepass medium -keypass medium

# Create truststore and import the CA cert.
keytool -keystore kafka.$i.truststore.jks -alias CARoot -import -file snakeoil-ca-1.crt -storepass medium -keypass medium

echo “medium” > ${i}_sslkey_creds
echo “medium” > ${i}_keystore_creds
echo “medium” > ${i}_truststore_creds
done
```

This script eventually generated for us following files
- broker1.csr
- broker1-ca-signed.crt
- broker1_keystore_creds
- broker1_sslkey_creds
- broker1_trustore_creds
- kafka.broker1.keystore.jks
- kafka.broker1.trustore.jks
Store this file at some easily accessible place, because we are going to use it to start docker containers of Kafka and Zookeeper.

docker-compose.yml
```yml
version: '3'

services:
 zookeeper:
   image: confluentinc/cp-zookeeper:latest
   container_name: zookeper
   environment:
     ZOOKEEPER_CLIENT_PORT: 2181
     ZOOKEEPER_TICK_TIME: 2000
   ports:
     - 22181:2181
 kafka:
   image: confluentinc/cp-kafka:latest
   container_name: kafka
   depends_on:
     - zookeeper
   ports:
     - 29093:29093
   environment:
     KAFKA_BROKER_ID: 1
     KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
     KAFKA_ADVERTISED_LISTENERS: SSL://localhost:29093
     KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
     KAFKA_SSL_KEYSTORE_FILENAME: kafka.broker1.keystore.jks
     KAFKA_SSL_KEYSTORE_CREDENTIALS: broker1_keystore_creds
     KAFKA_SSL_KEY_CREDENTIALS: broker1_sslkey_creds
     KAFKA_SSL_TRUSTSTORE_FILENAME: kafka.broker1.truststore.jks
     KAFKA_SSL_ENDPOINT_IDENTIFICATION_ALGORITHM: " "
     KAFKA_SSL_TRUSTSTORE_CREDENTIALS: broker1_truststore_creds
     KAFKA_SSL_CLIENT_AUTH: requested
     KAFKA_SECURITY_INTER_BROKER_PROTOCOL: SSL
     volumes:
       - ./secrets:/etc/kafka/secret
```

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/spring-boot-kafka-https-6d5765762256" >}}
{{< /cards >}}
