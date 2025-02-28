---
layout: post
title: "OpenGpts"
categories: gets
tags: opengpts
---

# OpenGPTs

## Quickstart with Docker

### Clone the Repository:

```sh
git clone https://github.com/langchain-ai/opengpts.git
cd opengpts
```

### Set Up Environment Variables:

Create a .env file in the root directory of the project by copying .env.example as a template, and add the following environment variables:

```sh
# At least one language model API key is required
OPENAI_API_KEY=placeholder

# Setup for Postgres. Docker compose will use these values to set up the database.
POSTGRES_PORT=5432
POSTGRES_DB=opengpts
POSTGRES_USER=postgres
POSTGRES_PASSWORD=placeholder
```

Replace placeholder with your OpenAI API key

### Run with Docker Compose:

```sh
docker compose up
```

