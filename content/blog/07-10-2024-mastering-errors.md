---
title: Mastering Error Handling in Spring Boot with ProblemDetails
type: blog
sidebar:
  open: true
date: 2024-09-26
comments: true
---

![Mastering error](/images/mastering-errors/mastering-error-1.png "Image by author")

### Introduction
Hello everyone! In this article I will try to cover a game — changer for
API error handling in Spring Boot — the ProblemDetails RFC.
If you spent a long time wrestling with inconsistent error responses
or scratching your head over how to structure your API’s error message,
you’re in for a treat.

### What is the deal with ProblemDetails?
![Spring Boot and Problem Details](/images/mastering-errors/mastering-error-2.png "Spring Boot + ProblemDetails")
First of all the ProblemDetails is not just another Spring Boot feature — it is an IETF standard (RFC 9457) that defines a “problem detail” as a way to carry machine-readable details error in a HTTP response.

Since Spring Boot 3.0 the ProblemDetails are natively supported, making it easier than ever to implement this standard in your applications. Before diving
into implementation details let’s answer the question “Why you should care?”

- Better client — side error handling
- Improved API documentation
- Consistency across your services

### Implementation
In this article, I’m using Spring Boot 3.3.4 where ProblemDetails is enabled by default. If you are using an older
version of Spring Boot you have to configure ProblemDetails manually.

```java {filename="ProblemDetailsConfig.java"}
package me.vrnsky.problemdetails.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

@Configuration
public class ProblemDetailsConfig {

    @Bean
    public ResponseEntityExceptionHandler exceptionHandler() {
      return new ResponseEntityExceptionHandler() {
        @Override
        protected ResponseEntity<Object> handleException(Exception exception,
            @Nullable Object body, HttpHeaders headers, HttpStatusCode statusCode,
            WebRequest request) {
           ProblemDetail problemDetail = ProblemDetail.forStatusAndDetail(statusCode, ex.getMessage());
           problemDetail.setProperty("timestamp", Instant.now());
           problemDetail.setProperty("exception", ex.getClass().getName());

           return super.handleExceptionInternal(ex, problemDetail, headers, statusCode, request);
    }
}
```

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/mastering-error-handling-in-spring-boot-with-problemdetails-33eac63a2888" >}}
{{< card icon="substack" title="Subtack" subtitle="Subscribe & read" link="https://vrnsky.substack.com/p/mastering-error-handling-in-spring" >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)

### Status Hub
Status Hub is simple uptime monitoring for your business. Start your free trial today!
Have a question? We are ready to answer!
{{< cards cols="2" >}}
{{< card link="https://statushub.app?utm_source=https://vrnsky.dev&utm_medium=blog" title="Start your 2 weeks free trial" icon="beaker" subtitle="No credit card required" >}}
{{< card link="mailto:support@statushub.app" title="Have a question?" icon="mail" subtitle="Ask us" >}}
{{< /cards >}}
