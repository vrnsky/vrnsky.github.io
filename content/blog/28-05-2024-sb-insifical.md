---
title: Spring Boot & Infisical - Managing your sensitive configuration
type: blog
sidebar:
  open: true
date: 2024-05-30
comments: true
---

Hello everyone! In this article, I’ll show you how to employ
Infisical in your Spring Boot application.

But last year, HashiCorp changed Terraform’s license to non-open source.
This could also happen to Vault, or not.
The second reason why I chose Infisical for this article is because
IBM acquired Terraform this year.

### Introduction
Like the HashiCorp Vault, Infisical is a secret management platform.
Let’s start by starting up the Infisical instance locally with the docker-compose
file provided by the documentation. First, we need to download it with the following command.

```bash
curl -o docker-compose.prod.yml https://raw.githubusercontent.com/Infisical/infisical/main/docker-compose.prod.yml
```

The second step is to get the .env file.
We can do it by command provided by the documentation.
```bash
curl -o .env https://raw.githubusercontent.com/Infisical/infisical/main/.env.example
```

Now we can start an instance of Infisical.
```bash
docker-compose -f docker-compose.yml up
```

After that, you should see this screen at `localhost:8080`

![Infisical](/images/infisical/infisical-1.png "Login page")

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/spring-boot-infisical-managing-your-sensitive-configuration-5ecfe9a5db08" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://vrnsky.substack.com/p/spring-boot-and-infisical-managing" >}}
{{< /cards >}}
