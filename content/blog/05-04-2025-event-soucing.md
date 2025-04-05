---
title: Event sourcing with Spring Boot, Kafka and jOOQ
type: blog
sidebar:
  open: true
date: 2025-04-05
comments: true
---

![Events arounds](/images/2025-04-05-sourcing/events-around.png "Events around")


One way of building resilient, scalable, and maintainable applications is use event sourcing. The event sourcing become a powerful architectural pattern. In classical approach we have only current state of application. On other hands in the event sourcing persist every state change as event. With this method we have complete history of changes. The complete history of changes easing debug, audit, and even reconstruction application state.


In this article we'll walk through implementation of event sourcing pattern. We'll develop Spring Boot application for a food delivery domain. During development we'll use Kafka as our event streaming platform. For robust data serialization we'll use Apache Avro and Schema Registry. jOOQ for database operations. We'll explore both theoretical aspects and practical implementation. By the end of article you will have understanding of how to apply event sourcing in you own projects.

### Understanding event sourcing
First, let's understand what is event sourcing and why it's especially powerful.
In traditional CRUD (Create, Read, Update, and Delete) application, we store the current state straight in database. When we need to update an object, we overwrite it previous state. The direct approach has limitation. Once history of changes lost, it will hard to understand how objects reached its current state.
Event sourcing takes a different approach:
- Every change to the application state is captured as an event.
- These events are stored in append - only event store.
- The current state is reconstructed by replacing these events.

When we add Kafka, Avro, Schema Registry, and jOOQ to this architecture, we gain benefits.
- Kafka provides distributed, fault - tolerant event streaming platform.
- Avro offers a compact, binary serialization format with robust schema support.
- Schema Registry ensures schema compatibility across producers and consumers.
-jOOQ provides type-safe SQL generation and execution, giving us more control over database operations than JPA.

For example, in a food delivery application, event like `OrderCreated`, `OrderAccepted`, or `OrderDelivered` are published to Kafka topics using Avro-defined schemas. These events are also stored in a database.

### Key benefits of this approach
- Complete audit trail: You have record of every change made to your system.
Schema evolution: Avro and Schema Registry enables safe evolution of you event schemas.
- Type-safe SQL: jOOQ provides compile-time checking of SQL queries.
- Compact serialization: Avro provides efficient binary serialization compared to JSON.
- Strong typing: Avro schemas and jOOQ provide type safety for your events.
- Real-time processing: Service can react to events immediately as they occur.
- Scalability: Kafka's distributed nature allows for high-throughput event processing.
- SQL control: jOOQ gives you precise control over your SQL without sacrificing type safety.

### Challenges to consider
- Operational complexity: Managing Kafka cluster and Schema Registry add operational overhead.
- Learning curve: Understanding Avro schemas, jOOQ, and event sourcing patterns takes time.
- Schema design: Careful planning is required for schema evolution strategies.
- Eventual consistency: The current state might not immediately available after events are stored.

### Implement event sourcing
Now, let's build a Spring Boot application that implements event sourcing for
a food delivery service using all mentioned tools.

#### Setting up the project
```xml {filename="pom.xml"}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.4.4</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>dev.vrnsky</groupId>
    <artifactId>event-sourcing</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>event-sourcing</name>
    <description>event-sourcing</description>
    <properties>
        <java.version>21</java.version>
        <avro.version>1.11.1</avro.version>
        <confluent.version>7.4.0</confluent.version>
        <jooq.version>3.20.2</jooq.version>
        <spring.datasource.url>jdbc:postgresql://localhost:51432/food_delivery</spring.datasource.url>
        <spring.datasource.username>postgres</spring.datasource.username>
        <spring.datasource.password>postgres</spring.datasource.password>
        <liquibase.version>4.31.1</liquibase.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jooq</artifactId>
        </dependency>

        <!-- Kafka -->
        <dependency>
            <groupId>org.springframework.kafka</groupId>
            <artifactId>spring-kafka</artifactId>
        </dependency>

        <!-- Avro and Schema Registry -->
        <dependency>
            <groupId>org.apache.avro</groupId>
            <artifactId>avro</artifactId>
            <version>${avro.version}</version>
        </dependency>
        <dependency>
            <groupId>io.confluent</groupId>
            <artifactId>kafka-avro-serializer</artifactId>
            <version>${confluent.version}</version>
        </dependency>
        <dependency>
            <groupId>io.confluent</groupId>
            <artifactId>kafka-schema-registry-client</artifactId>
            <version>${confluent.version}</version>
        </dependency>

        <!-- Database -->
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
        </dependency>
        <dependency>
            <groupId>org.liquibase</groupId>
            <artifactId>liquibase-core</artifactId>
            <version>${liquibase.version}</version>
        </dependency>

        <!-- Utilities -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.jetbrains</groupId>
            <artifactId>annotations</artifactId>
            <version>26.0.2</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                    <annotationProcessorPaths>
                        <path>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                            <version>1.18.36</version>
                        </path>
                    </annotationProcessorPaths>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <!-- Avro Schema Generation -->
            <plugin>
                <groupId>org.apache.avro</groupId>
                <artifactId>avro-maven-plugin</artifactId>
                <version>${avro.version}</version>
                <executions>
                    <execution>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>schema</goal>
                        </goals>
                        <configuration>
                            <sourceDirectory>${project.basedir}/src/main/avro</sourceDirectory>
                            <outputDirectory>${project.build.directory}/generated-sources/avro</outputDirectory>
                            <stringType>String</stringType>
                            <imports>
                                <import>${project.basedir}/src/main/avro/BaseEvent.avsc</import>
                            </imports>
                        </configuration>
                    </execution>
                </executions>
            </plugin>

            <!-- Liquibase Plugin -->
            <plugin>
                <groupId>org.liquibase</groupId>
                <artifactId>liquibase-maven-plugin</artifactId>
                <version>${liquibase.version}</version>
                <configuration>
                    <changeLogFile>src/main/resources/db/changelog.yml</changeLogFile>
                    <url>${spring.datasource.url}</url>
                    <username>${spring.datasource.username}</username>
                    <password>${spring.datasource.password}</password>
                </configuration>
                <executions>
                    <execution>
                        <phase>initialize</phase>
                        <goals>
                            <goal>update</goal>
                        </goals>
                    </execution>
                </executions>
                <dependencies>
                    <dependency>
                        <groupId>org.postgresql</groupId>
                        <artifactId>postgresql</artifactId>
                        <version>${postgresql.version}</version>
                    </dependency>
                </dependencies>
            </plugin>

            <!-- jOOQ Code Generation -->
            <plugin>
                <groupId>org.jooq</groupId>
                <artifactId>jooq-codegen-maven</artifactId>
                <version>${jooq.version}</version>
                <executions>
                    <execution>
                        <id>jooq-codegen</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>generate</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <jdbc>
                        <driver>org.postgresql.Driver</driver>
                        <url>${spring.datasource.url}</url>
                        <user>${spring.datasource.username}</user>
                        <password>${spring.datasource.password}</password>
                    </jdbc>
                    <generator>
                        <generate>
                            <tables>true</tables>
                        </generate>
                        <database>
                            <name>org.jooq.meta.postgres.PostgresDatabase</name>
                            <includes>.*</includes>
                            <excludes>databasechangelog|databasechangeloglock</excludes>
                            <inputSchema>public</inputSchema>
                        </database>
                        <target>
                            <packageName>dev.vrnsky.eventsourcing.db.generated</packageName>
                            <directory>${project.build.directory}/generated-sources/jooq</directory>
                        </target>
                    </generator>
                </configuration>
                <dependencies>
                    <dependency>
                        <groupId>org.postgresql</groupId>
                        <artifactId>postgresql</artifactId>
                        <version>${postgresql.version}</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>

    <repositories>
        <repository>
            <id>confluent</id>
            <url>https://packages.confluent.io/maven/</url>
        </repository>
    </repositories>

</project>
```

#### Defining Avro schemas
Let's define our Avro schemas for the food delivery events. We'll
place these in `src/main/avro` directory. First, let's crate base event schema
(`src/main/avro/BaseEvent.avsc`)

### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/event-sourcing-with-spring-boot-kafka-and-jooq-5901455c3f32" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/event-sourcing-with-spring-boot-kafka?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/event-sourcing-with-spring-boot-kafka-and-jooq/"  >}}
{{< card icon="craft" title="Craft" subtitle="Buy password & read" link="https://vrnsky.craft.me/1WrWfqw77nNrk8"  >}}
{{< /cards >}}
