---
title: Spring Boot Mutation testing with JUnit5, Testcontainers, and Pit
type: blog
sidebar:
  open: true
date: 2023-12-13
---

### What is mutation testing?
Mutation testing is a type of testing that validates new and existing tests. More formal definition from [Wikipedia](https://en.wikipedia.org/wiki/Mutation_testing):
> Mutation testing (or mutation analysis or program mutation) is
> used to design new software tests and evaluate the quality of existing software tests.

### Why do we need mutation testing?
The problem that solves mutation testing is checking the validity of the existing and new tests. 
I often have met invalid unit tests that have covered only the happy path and no other paths.

### When does it make sense for mutation testing?
So, if overall coverage is below 80%, you can skip mutation testing. 
You can return to mutation testing once you reach a threshold of 80% coverage.

### How is mutation testing working?
The mutation testing itself is a form of white box testing. More or less mutation testing,
trying to mutate or change your code and check that unit tests will fail.
The process of changing your code is called mutation. 
The mutation can be killed or survived during the test phase. The killed mutation is a good sign,
notifying us that the unit tests caught the mutation and failed the unit test; on the other hand,
if the mutation survived, that is a bad sign that the unit test did not die with code changes.

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/spring-boot-mutation-testing-with-junit-5-testcontainiers-and-pit-1f70e22753ef" >}}
{{< /cards >}}