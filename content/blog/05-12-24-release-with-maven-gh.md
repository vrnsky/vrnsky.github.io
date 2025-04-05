---
title: Master Java Release with GitHub Actions and Maven Release plugin
type: blog
sidebar:
  open: true
date: 2024-12-05
comments: true
---
### Introduction

In software development, automating the release process is key. It ensures efficiency and consistency in a fast-paced field.
Many Java developer struggle with manual release. They face issues with version management and Git tagging. This article will
show you how to automate your release process using GitHub Actions and the Maven Release plugin

### Prerequisites
Before diving into the implementation, ensure you have
- A Java project using Maven.
- A GitHub repository.
- Basic understanding of GitHub Actions
- Admin access to your repository.

### Maven Release plugin overview
The Maven release plugin helps automate the release process of Maven projects. It handles version updates, git tagging,
and deployment of release artifacts. Key benefits include:
- Automated version management.
- Consistent git tagging.
- Build-in rollback mechanisms.
- Integration with dependency management.

### Let's roll
Let's configure the plugin in your pom.xml.
```xml
<project>
    <!-- Other POM configurations -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-release-plugin</artifactId>
                <version>3.0.1</version>
                <configuration>
                    <tagNameFormat>v@{project.version}</tagNameFormat>
                    <checkModificationExcludes>
                        <checkModificationExclude>pom.xml</checkModificationExclude>
                    </checkModificationExcludes>
                    <pushChanges>false</pushChanges>
                    <localCheckout>true</localCheckout>
                    <goals>deploy</goals>
                </configuration>
            </plugin>
        </plugins>
    </build>
<!-- Distribution management is required -->
<distributionManagement>
  <repository>
    <id>github</id>
    <name>GitHub Packages</name>
    <url>https://maven.pkg.github.com/${github.repository}</url>
    </repository>
</distributionManagement>
<scm>
  <developerConnection>scm:git:https://github.com/username/repository.git</developerConnection>
  <tag>HEAD</tag>
</scm>
</project>
```

### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/master-java-releases-with-github-actions-and-maven-release-plugin-0a6fce46a2d7" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://vrnsky.substack.com/p/master-java-releases-with-github"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/master-java-releases-with-github-actions-and-maven-release-plugin/"  >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)
