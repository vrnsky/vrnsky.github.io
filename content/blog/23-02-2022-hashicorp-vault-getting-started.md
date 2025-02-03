---
title: HashiCorp Vault - Getting started
type: blog
sidebar:
  open: true
date: 2022-02-23
comments: true
---

Hi, there! It is a text version of the Vault webinar

Let’s go!

First of all, we have to download Vault or install it via your favorite packet manager. You can download the latest version of Vault from the official website — https://www.vaultproject.io/downloads

Or simply install it via brew
```bash
brew tap hashicorp/tap
brew install hashicorp/tap/vault
```

After successful installation, we can check that Vault in the PATH
![PATH image](hashicorp-1.png)

In this tutorial, we are going to use Consul as the backend for our Vault. The Consuls is basically key-value storage

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/consul
```

After this, we can check that installation was successful
![Consul Working](consul-1.png)

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/hashicorp-vault-getting-started-4a3b7d4abf48" >}}
{{< /cards >}}
