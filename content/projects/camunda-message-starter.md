---
title: Camunda Message Spring Boot Starter
type: docs
sidebar:
  open: true
next: java-a-to-z
---

### Project description
Send message to Camunda, it is trivial task, but it brings a lot of boilerplate code.
By using this project you can save you time.

### Usage
```xml
<dependency>
    <groupId>io.vrnsky</groupId>
    <artifactId>camunda-messaging-starter</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

### Local development

```bash
mvn clean kotlin:compile install
```

Spring beans configured automatically create required beans, but as usual you can override
this behavior

```java {filename="MessageConfiguration.java"}
import io.vrnsky.camunda.messaging.starter.CamundaMessageConfiguration;
import io.vrnsky.camunda.messaging.starter.CamundaMessageTemplate;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MessageConfiguration {

    @Bean
    public CamundaMessageTemplate camundaMessageTemplate() {
        var camundaMessageConfiguration = new CamundaMessageConfiguration("http://localhost:8080");
        return new CamundaMessageTemplate(camundaMessageConfiguration);
    }
}
```

Example of usage

```java {filename="CamundaController.java"}
import io.vrnsky.camunda.messaging.starter.CamundaMessageTemplate;
import io.vrnsky.camunda.messaging.starter.model.CamundaMessage;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class CamundaController {

    @Autowired
    private CamundaMessageTemplate camundaMessageTemplate;

    @PostMapping("/message")
    public void message(@RequestBody CamundaMessage camundaMessage) {
        camundaMessageTemplate.message(camundaMessage);
    }
}
```

In logs you should see something like this

```text
CamundaMessageTemplate   : baseUrl obtained from configs = http://localhost:8080
```