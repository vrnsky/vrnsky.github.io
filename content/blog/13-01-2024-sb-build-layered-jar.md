---
title: Spring Boot - How to build layered jar
type: blog
sidebar:
  open: true
date: 2024-01-06
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
{{< cards >}}
{{< card icon="medium" title="Medium" subtitle="Read full article" link="https://medium.com/@vrnsky/spring-boot-how-to-build-layered-jar-81bfe6d843f6" >}}
{{< card icon="substack" title="Substack" subtitle="Read full article" link="https://vrnsky.substack.com/p/spring-boot-how-to-build-layered" >}}
{{< /cards >}}

