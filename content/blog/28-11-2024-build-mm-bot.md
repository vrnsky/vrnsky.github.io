---
title: Build a MatterMost Bot with Java - Practical guide
type: blog
sidebar:
  open: true
date: 2024-11-28
comments: true
---

### Introduction
Weather info in your team chat can help with office planning and casual chats.
This article will build a simple, practical MatterMost bot. It will post
daily weather updates using Java, Spring Boot, and weather API.

### What we will build
Spring Boot application that:
- Connects to MatterMost via webhooks.
- Fetches weather data from OpenWeatherMap API.
- Posts daily weather updates at 9:00 AM.

### Prerequisites
- Java 17
- Maven or Gradle
- Docker

### Implementation
Let's start bot development using the MatterMost server on our local environment.
Create a docker-compose file with the following content.

```yaml
version: '3'
services:
  postgres:
    image: postgres:14-alpine
    container_name: mattermost-postgres
    environment:
      - POSTGRES_USER=mmuser
      - POSTGRES_PASSWORD=mmuser_password
      - POSTGRES_DB=mattermost
    volumes:
      - mattermost-postgres:/var/lib/postgresql/data
    networks:
      - mattermost-network

  mattermost:
    image: mattermost/mattermost-team-edition:latest
    container_name: mattermost-server
    depends_on:
      - postgres
    environment:
      # Database configuration
      - MM_SQLSETTINGS_DRIVERNAME=postgres
      - MM_SQLSETTINGS_DATASOURCE=postgres://mmuser:mmuser_password@postgres:5432/mattermost?sslmode=disable
      # Server settings
      - MM_SERVICESETTINGS_SITEURL=http://localhost:8065
      # SMTP settings (if needed)
      - MM_EMAILSETTINGS_ENABLESMTPAUTH=false
      - MM_EMAILSETTINGS_PUSHNOTIFICATIONCONTENTS=generic
      # File storage settings
      - MM_FILESETTINGS_DIRECTORY=/mattermost/data
      # Log settings
      - MM_LOGSETTINGS_ENABLEFILE=true
      - MM_LOGSETTINGS_FILENAME=/mattermost/logs/mattermost.log
    volumes:
      - mattermost-data:/mattermost/data
      - mattermost-logs:/mattermost/logs
      - mattermost-plugins:/mattermost/plugins
      - mattermost-client-plugins:/mattermost/client/plugins
      - mattermost-bleve-indexes:/mattermost/bleve-indexes
    ports:
      - "8065:8065"
    networks:
      - mattermost-network

volumes:
  mattermost-postgres:
  mattermost-data:
  mattermost-logs:
  mattermost-plugins:
  mattermost-client-plugins:
  mattermost-bleve-indexes:

networks:
  mattermost-network:
    driver: bridge
```

Now, to run MatterMost execute the next command.
```bash
docker compose up
```

You can add the -d flag to run in detached mode, but for monitoring purposes, use attached mode. Open your browser and type http://localhost:8065. You should see
the home page of a running MatterMost instance.

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/bulid-a-mattermost-weather-bot-with-java-a-practical-guide-d293892e5c1f" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://vrnsky.substack.com/p/bulid-a-mattermost-weather-bot-with" >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)
