---
title: Know what dependency do you have
type: docs
sidebar:
  open: true
tags:
  - maven
comments: true
---

I quite often stuck in situations when some transitive dependencies break my project, so the first step of investigation is to know what dependencies are used by your project.
You can get information about your dependencies with following command

```bash
mvn dependency:tree
```
