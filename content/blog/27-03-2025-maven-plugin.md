---
title: Maven plugin development from basic to advanced
type: blog
sidebar:
  open: true
date: 2025-03-27
comments: true
---

![Extensions](/images/2025-03-27-maven-plugin/mvnplugin.png "Extensions")


### Introduction
Ever found yourself repeating the same mundane tasks during your build process? You might be checking for `SNAPSHOT` dependencies before a release. You could also check code formatting or do custom verifications that regular plugins don't handle. We developers love automation. Maven plugins help us do that. They let you tweak and customize your build process to match your project's need.

In this article, I'll guide you through creating your own Maven plugins, from simple to a sophisticated. After I missed SNAPSHOT dependencies during a release and caused production delay, I saw that a custom Maven plugin could fix this issue for good. Why manually check when you can automate?

### What is Maven plugin?
A Maven plugin is mainly a set of goals, also known as Mojos. These are Maven plain old Java objects that carry out specific tasks during the build lifecycle.
These plugins handle tasks such as:
- Compiling code.
- Running tests.
- Generating documentation.
- Deploying artifacts.

Here is how plugins fit into Maven's architecture:
Build lifecycle: Maven sets a standard build process. It includes phases like `validate`, `compile`, `test`, `package`, `install`, and `deploy`.
Plugins: plugin attach their goals to these lifecycle phases.
Goals: Each goal performs a specific task and can be assigned to one or more phases or executed directly.

Some popular plugins are the maven-compiler-plugin , used for compiling Java code, and the maven-surefire-plugin , which run tests. You might know these example well.
Getting started with plugin development
Let's start by creating a basic Maven plugin from scratch. We'll use Maven's archetype to generate the intial project structure.

```
mvn archetype:generate \
  -DgroupId=io.vrnsky \
  -DartifactId=maven-snapshot-detector \
  -Dversion=1.0.0-SNAPSHOT \
  -DarchetypeGroupId=org.apache.maven.archetypes \
  -DarchetypeArtifactId=maven-archetype-mojo
```

This command creates a project with the basic stucture needed for plugin development. The generated project includes a simple Mojo (goal implementation) that we will customize.

### Understanding the plugin structure
After running the archetype generator, you should have a project with this structure:
```
maven-snapshot-detector/
├── pom.xml
└── src/
    └── main/
        └── java/
            └── io/
                └── vrnsky/
                    └── MyMojo.java
```

Let's take a look at the generated pom.xml
```xml {filename="pom.xml", hl_lines=[8]}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>io.vrnsky</groupId>
  <artifactId>maven-snapshot-detector</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <packaging>maven-plugin</packaging>

  <name>maven-snapshot-detector Maven Mojo</name>
  <url>http://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-plugin-api</artifactId>
      <version>2.0</version>
    </dependency>
    <dependency>
      <groupId>org.apache.maven.plugin-tools</groupId>
      <artifactId>maven-plugin-annotations</artifactId>
      <version>3.2</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-project</artifactId>
      <version>2.0.6</version>
    </dependency>
  </dependencies>
</project>
```


### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/maven-plugin-development-from-basic-to-advanced-9b666dc55211" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/maven-plugin-development-from-basic?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/maven-plugin-development-from-basic-to-advanced/"  >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)

### Status Hub
Status Hub is simple uptime monitoring for your business. Start your free trial today!
Have a question? We are ready to answer!
{{< cards cols="2" >}}
{{< card link="https://statushub.app?utm_source=https://vrnsky.dev&utm_medium=blog" title="Start your 2 weeks free trial" icon="beaker" subtitle="No credit card required" >}}
{{< card link="mailto:support@statushub.app" title="Have a question?" icon="mail" subtitle="Ask us" >}}
{{< /cards >}}
