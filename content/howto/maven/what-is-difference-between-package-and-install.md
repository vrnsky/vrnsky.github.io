---
title: What is the difference between package and install in Maven?
type: docs
sidebar:
  open: true
tags:
  - maven
---

This question you may have heard or may ask during a job interview.
The difference is simple. The "package" goal only compiles, tests, and packages
your app into an archive, either a war or a jar.
The "install" goal does all the "package" goal and copies the compiled archive to your local repository `(~/.m2/repository/)`
