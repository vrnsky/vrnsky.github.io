---
title: Build Maven Project concurrently
type: docs
sidebar:
  open: true
next: build-maven-project-without-tests
tags:
  - maven
---

If you would like to run build of Maven project in concurrent mode you can use following command
```bash
mvn clean package -T X
```

where `X` - number of threads that will be using by Maven to build your project.

Example:
```bash
mvn clean package -X 4
```
