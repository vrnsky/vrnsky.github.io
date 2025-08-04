---
title: Spring Boot - How to build layered jar
type: blog
sidebar:
  open: true
date: 2024-01-06
comments: true
---
In this article, I will show you how you can build a simple CRUD application and create a layered jar.
The inventory service manages inventory, such as left stocks, i.e., some drinks, merch, or something else that can be stored in the warehouse.

Reasons for choosing layered jar:
- If you have an extensive application with different dependencies
- If you need flexibility in layer updates

Reasons for choosing Uber Jar:
- If you have a simple application with a relatively small number of dependencies
- If you need simplicity in the deployment process

```dockerfile {filename="Dockerfile"}
FROM eclipse-temurin:17 as JAR_EXTRACT
WORKDIR /app
ARG JAR_FILE=*.jar
COPY ./target/${JAR_FILE} ./app.jar
RUN java -Djarmode=layertools -jar ./app.jar extract
FROM eclipse-temurin:17
WORKDIR /application
COPY --from=JAR_EXTRACT /app/dependencies ./
COPY --from=JAR_EXTRACT /app/spring-boot-loader ./
COPY --from=JAR_EXTRACT /app/snapshot-dependencies ./
COPY --from=JAR_EXTRACT /app/application ./
ENTRYPOINT ["java", "org.springframework.boot.loader.launch.JarLauncher"]
EXPOSE 8080
```

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/spring-boot-how-to-build-layered-jar-81bfe6d843f6" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://vrnsky.substack.com/p/spring-boot-how-to-build-layered" >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)

### Status Hub
Status Hub is simple uptime monitoring for your business. Start your free trial today!
Have a question? We are ready to answer!
{{< cards cols="2" >}}
{{< card link="https://statushub.app?utm_source=https://vrnsky.dev&utm_medium=blog" title="Start your 2 weeks free trial" icon="beaker" subtitle="No credit card required" >}}
{{< card link="mailto:support@statushub.app" title="Have a question?" icon="mail" subtitle="Ask us" >}}
{{< /cards >}}
