---
title: JUnit 5 - How to write more test with less code
type: blog
sidebar:
  open: true
date: 2023-12-31
comments: true
---

### Introduction
In this article, I will show and explain how you can write more tests with relatively small changes in your code.
Recently, one of my colleagues wrote a massive test with repetitive code.
The difference between test cases was only data that was submitted to the service.
I will use JUnit 5 in this article, but feel free to check the library docs you use for writing tests.

### Problem
Let’s imagine the following situation: we have a service that
accepts the following data and returns the following response.

```json {filename="request.json"}
{
  "operationType": "+",
  "operands": [
    1,
    2,
    3,
    4,
    5
  ]
}
```
```json {filename="response.json"}
{
  "result": 15
}
```

Of course, we can write many tests to cover each aspect, but there is a better solution.
Let me introduce to you TestFactory from JUnit 5. You may argue that artificial cases use
a test factory, and I agree with you, but the article is designed to give you an idea
of how you can achieve more tests without writing more code.

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/junit-5-how-to-write-more-tests-with-less-code-23aea5e7ee16" >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)
