---
title: Structured logging
type: blog
sidebar:
  open: true
date: 2025-03-23
comments: true
---

Spring Boot 3.4 adds native support for structured logging. This makes it easier to create machine — readable logs that work well with log aggregation tools. In this quick guide, I’ll show you how to configure and use this powerful feature.

### What is structured logging?
Traditional text — based logs are great for humans but challenging for machines to parse. Structured logging formats logs as JSON objects. These have defined fields, makint them easier to search, filter, and analyze. You can use tools like ELK Stack.
Setting up structured logging

#### Step 1. Add dependencies
For a Spring Boot 3.4+ application, you don’t need any addtional dependencies as structured logging suports is included.

#### Step 2. Configure the application through application.yml or application.properties
```yaml {filename="application.yml"}
logging:
  structured:
    format:
      console: logstash
    json:
      exclude: "@version"
      add:
        app-name: logging-app
        app-version: "@project.version@"
```

Step 3. Use logger in your codepackage io.vrnsky.logging.controller;

```java {filename="EchoController.java"}
import java.util.Map;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class EchoController {

    private static final Logger logger = LoggerFactory.getLogger(
        EchoController.class
    );

    @GetMapping("/example")
    public String example() {
        logger.info("Processing request with id={}", "abc123");

        logger.info(
            "Order processed successfully",
            Map.of(
                "orderId",
                "ORD-12345",
                "amount",
                199.99,
                "customer",
                "customer-456"
            )
        );

        return "Example response";
    }
}
```



#### Sample JSON output
```json
{"@timestamp":"2025-03-23T16:13:18.404721+03:00","message":"Processing request with id=abc123","logger_name":"io.vrnsky.logging.controller.EchoController","thread_name":"http-nio-8080-exec-1","level":"INFO","level_value":20000,"app-name":"logging-app","app-version":"0.0.1-SNAPSHOT"}
{"@timestamp":"2025-03-23T16:13:18.405554+03:00","message":"Order processed successfully","logger_name":"io.vrnsky.logging.controller.EchoController","thread_name":"http-nio-8080-exec-1","level":"INFO","level_value":20000,"app-name":"logging-app","app-version":"0.0.1-SNAPSHOT"}
```


### Benefits of using structured logging
- Improved searchability: find specific log entries based on each field values.
- Better analysis aggregate and analyze logs based on structured fields.
- Monitoring enhancement: Create more precise alerts and visualizations
- Consistent format: Standardized format across your entire application

If you need more control, Spring Boot allows advanced customization through `logback-spring.xml`

### Conclusion
Structured logging in Spring Boot 3.4. makes it significantly easier to adopt modern logging practices. With minimal configuration, you can transform your application logs into a format that’s ready for enterpirse — grade log.
Remember that structured logging works best when paired with a log aggregation system like ELK Stack or Grafana Loki. The real power comes when you can easily query and visualize your logs at scale.

Happy coding!
