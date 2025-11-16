---
title: "Docker Compose Health Check"
description: "A simple health check configuration for Docker Compose services"
publishDate: 2024-11-16
language: "yaml"
category: "docker"
tags: ["docker", "docker-compose", "health-check", "devops"]
draft: false
---

Here's a handy Docker Compose health check configuration that I use frequently:

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    healthcheck:
      test: ["CMD", "wget", "--no-verbose", "--tries=1", "--spider", "http://localhost/"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
    depends_on:
      api:
        condition: service_healthy

  api:
    image: node:18-alpine
    ports:
      - "3000:3000"
    healthcheck:
      test: ["CMD", "wget", "--no-verbose", "--tries=1", "--spider", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

## Key Points

- **`interval`**: How often to run the health check
- **`timeout`**: How long to wait for a response
- **`retries`**: Number of consecutive failures before marking as unhealthy
- **`start_period`**: Grace period before health checks start
- **`depends_on: condition: service_healthy`**: Wait for dependencies to be healthy

This ensures services start in the right order and are actually ready before dependent services try to connect.