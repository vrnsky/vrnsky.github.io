---
title: Write your Spring Boot (3.x) starter with Kotlin & Maven
type: blog
sidebar:
  open: true
date: 2023-01-23
---

Some companies use [Camunda(TM) BPMN Engine](https://camunda.com/) for managing the business automatization process. Most of the functionality provided out of the box is enough for most cases. But recently I have realized that we have always written our service to send messages to the engine.
So, I decided to write my starter. The native language for Camunda is Java, but it supports many other languages. Since I want programming experience in Java, I have decided to write my starter with Kotlin.
For those who are already tired — the full code is available on the GitHub
There are no breaking backward capability changes in writing spring boot starters.

Changes:

Now auto configurations load from another file placed at resources/META-INF/spring/packageName.className.imports. Don’t worry old way of spring.factories work too
I decided to use Maven as a build tool, so it is my pom.xml file

```xml {filname="pom.xml"}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>io.vrnsky</groupId>
    <artifactId>camunda-messaging-starter</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>camunda-messaging-starter</name>
    <description>Message Camunda without overhead</description>

    <properties>
        <java.version>17</java.version>
        <kotlin.version>1.7.22</kotlin.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
            <version>3.0.2</version>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.0.2</version>
        </dependency>

        <dependency>
            <groupId>com.fasterxml.jackson.module</groupId>
            <artifactId>jackson-module-kotlin</artifactId>
            <version>2.14.1</version>
        </dependency>
        <dependency>
            <groupId>org.jetbrains.kotlin</groupId>
            <artifactId>kotlin-reflect</artifactId>
            <version>1.8.0</version>
        </dependency>
        <dependency>
            <groupId>org.jetbrains.kotlin</groupId>
            <artifactId>kotlin-stdlib-jdk8</artifactId>
            <version>1.8.0</version>
        </dependency>

        <dependency>
            <groupId>org.jetbrains.kotlin</groupId>
            <artifactId>kotlin-maven-lombok</artifactId>
            <version>${kotlin.version}</version>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.24</version>
            <scope>provided</scope>
        </dependency>

        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-api</artifactId>
            <version>2.19.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.19.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-slf4j-impl</artifactId>
            <version>2.19.0</version>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-source-plugin</artifactId>
                <version>3.2.1</version>
            </plugin>
            <plugin>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-maven-plugin</artifactId>
                <version>1.7.22</version>
                <configuration>
                    <sourceDirs>
                        <sourceDir>${project.basedir}/src/main/kotlin</sourceDir>
                    </sourceDirs>
                    <args>
                        <arg>-Xjsr305=strict</arg>
                    </args>
                </configuration>
                <dependencies>
                    <dependency>
                        <groupId>org.jetbrains.kotlin</groupId>
                        <artifactId>kotlin-maven-allopen</artifactId>
                        <version>${kotlin.version}</version>
                    </dependency>
                </dependencies>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.5.1</version>
                <configuration>
                    <source>17</source>
                    <target>17</target>
                    <annotationProcessorPaths>
                        <annotationProcessorPath>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                            <version>1.18.24</version>
                        </annotationProcessorPath>
                    </annotationProcessorPaths>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```
We use some dependency as spring-boot-web-starter because we need RestTemplate class for HTTP calls. There are dependencies for Kotlin and Logging. 
For building projects, I use the following command

```bash
mvn clean kotlin:compile install
```

So, let’s start with defining model classes of objects which start will be working with. 
Before we start writing code — I strongly advise checking the actual [documentation of Camunda messaging](https://docs.camunda.org/manual/7.16/reference/rest/message/post-message/).

```kolin
enum class VariableType {
    Json, String
}
```

So we can have two types of variables — json and string types

```kotlin
data class ProcessVariable(
    val value: String,
    val type: VariableType
) {}
```
This class describes process variables — which widely used in Camunda

```kotlin
data class CamundaMessage(
    val businessKey: String,
    val messageName: String,
    val correlationKeys: Map<String, VariableType>,
    val processVariables: Map<String, VariableType>
) {
}
```

### Access full article
{{< cards >}}
{{< card icon="medium" link="https://medium.com/@vrnsky/write-your-spring-boot-3-x-starter-with-kotlin-maven-a75f367c6254" title="Read full article on Medium" >}}
{{< /cards >}}