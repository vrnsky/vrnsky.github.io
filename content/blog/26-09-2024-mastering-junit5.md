---
title: Mastering JUnit 5 - Advanced Techniques for Efficient and Powerful testing
type: blog
sidebar:
  open: true
date: 2024-09-24
comments: true
---

![Meme about unit test](/images/junit/meme-1.png "Meme about unit tests")

Hello everyone in this article we will dive into note-worthy JUnit 5
annotations which help you to write extensive unit tests.

Before starting to start writing unit tests we have to add
required dependencies to our pom.xml or build.gradle.

```xml {filename="pom.xml"}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>me.vrnsky</groupId>
    <artifactId>mastering-junit</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-params</artifactId>
            <version>5.11.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.11.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.11.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

### Parametrized test
This article will follow test — driven development approach,
so first, we will write a unit test. Most of the examples of test units
contain examples of testing simple calculators, but for this example,
we will develop a String utility class.

This type of tests allow to run the same test multiple times with
different argument. It helps developers reduce code duplications and provide
more comprehensive testing with less effort.

```java {filename="StringUtilsTest.java"}
package me.vrnsky;

import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;

class StringUtilsTest {

    @ParameterizedTest
    @CsvSource(value = {"a, 1, a", "b, 3, bbb", "c, 0, ''"})
    void testThatStringUtilsRepeatProduceCorrectOutput(String input, int count, String expected) {
        Assertions.assertEquals(expected, StringUtils.repeat(input, count));
    }
}
```
### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/mastering-junit-5-advanced-techniques-for-efficient-and-powerful-testing-0203992bdb95" >}}
{{< card icon="substack" title="Subtack" subtitle="Subscribe & read" link="https://vrnsky.substack.com/p/mastering-junit-5-advanced-techniques" >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)

### Status Hub
Status Hub is simple uptime monitoring for your business. Start your free trial today!
Have a question? We are ready to answer!
{{< cards cols="2" >}}
{{< card link="https://statushub.app?utm_source=https://vrnsky.dev&utm_medium=blog" title="Start your 2 weeks free trial" icon="beaker" subtitle="No credit card required" >}}
{{< card link="mailto:support@statushub.app" title="Have a question?" icon="mail" subtitle="Ask us" >}}
{{< /cards >}}