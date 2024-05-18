# DOCKER DOCUMENTATION
Here's a `README.md` file for the provided Dockerfile setup:

```markdown
# Real Estate Project Development Docker Image

This repository contains the Docker setup for the Real Estate Project. The Dockerfile is based on the `python:3.10.0-slim-buster` image and sets up the environment for developing the project.

## Dockerfile Overview

The Dockerfile performs the following tasks:
- Sets up the base image and environment variables.
- Installs necessary system dependencies.
- Upgrades `pip`.
- Copies and installs Python dependencies from `requirements.txt`.
- Prepares entrypoint and start scripts for running the application.

## Dockerfile Contents

```dockerfile
FROM python:3.10.0-slim-buster

ENV APP_HOME=/app
RUN mkdir $APP_HOME
RUN mkdir $APP_HOME/staticfiles
WORKDIR $APP_HOME

LABEL maintainer='api.imperfect@gmail.com'
LABEL youtube="https://www.youtube.com/c/APIImperfect"
LABEL description="Development image for Real Estate Project"

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update \
  && apt-get install -y build-essential \
  && apt-get install -y libpq-dev \
  && apt-get install -y gettext \
  && apt-get -y install netcat gcc postgresql \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip

COPY ./requirements.txt /app/requirements.txt 
RUN pip3 install -r requirements.txt

COPY ./docker/local/django/entrypoint /entrypoint
RUN sed -i 's/\r$//g' /entrypoint
RUN chmod +x /entrypoint

COPY ./docker/local/django/start /start
RUN sed -i 's/\r$//g' /start
RUN chmod +x /start

ENTRYPOINT [ "/entrypoint"]
```

### Entry Point Script

The `entrypoint` script is responsible for setting up the environment each time the container starts. Ensure that the script is executable and has Unix-style line endings.

### Start Script

The `start` script is used to run the Django development server. Like the `entrypoint` script, it must be executable and have Unix-style line endings.

## Environment Variables

- `PYTHONDONTWRITEBYTECODE`: Prevents Python from writing `.pyc` files to disk.
- `PYTHONUNBUFFERED`: Ensures that the Python output is sent straight to the terminal (without being buffered).

## Maintainer

- **USER**: Manjil Gautam [Destiny]





# Docker Compose Configuration for Real Estate Project

This document provides an overview and usage instructions for the Docker Compose configuration used in the Real Estate Project.

## Overview

The Docker Compose file defines services and their configurations for orchestrating the Real Estate Project environment. It sets up two services: `api` and `postgres-db`, facilitating the development and database requirements.

### Services

- **api**: Service for running the Real Estate Project API.
- **postgres-db**: PostgreSQL database service for storing project data.

## Getting Started

### Prerequisites

Ensure you have Docker and Docker Compose installed on your system. You can download Docker Desktop, which includes Docker Compose, from [here](https://www.docker.com/products/docker-desktop).

### Configuration

The Docker Compose configuration includes the following sections:

```yaml

version: '3.8'

services:
    api:
        build:
            context: .
            dockerfile: ./docker/local/django/Dockerfile
        command: /start
        volumes:
            - .:/app
            - static_volume:/app/staticfiles
            - media_volume:/app/mediafiles
        ports:  # Use ports instead of expose
            - "8000:8000"
        env_file:
            - .env
        depends_on:
            - postgres-db
        networks:
            - estate-react

    postgres-db:
        image: postgres:12.0-alpine
        ports:
            - "5432:5432"
        volumes:
            - postgres_data:/var/lib/postgresql/data/
        environment:
            - POSTGRES_USER=${POSTGRES_USER}
            - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
            - POSTGRES_DB=${POSTGRES_DB}
        networks:
            - estate-react

networks:
    estate-react:
        driver: bridge

volumes:
    postgres_data:
    static_volume:
    media_volume:

```
# Makefile Usage and Commands

This Makefile provides convenience commands for managing the Real Estate Project using Docker and Docker Compose.

## Prerequisites

Ensure you have Docker and Docker Compose installed on your system. You can download Docker Desktop, which includes Docker Compose, from [here](https://www.docker.com/products/docker-desktop).

## Configuration

The Makefile checks for the presence of a `.env` file and includes it if found. It then exports the variables defined in the `.env` file.

### Environment Variables

If you have a `.env` file in your project directory, the Makefile will automatically load and export its variables to be used by Docker Compose.

## Commands

- `build`: Builds the Docker containers, ensuring they are up-to-date. Usage: `make build`
- `up`: Starts the Docker containers in detached mode. Usage: `make up`
- `down`: Stops and removes the Docker containers. Usage: `make down`
- `show-logs`: Displays the logs of the Docker containers. Usage: `make show-logs`
- `migrate`: Runs Django database migrations. Usage: `make migrate`
- `makemigrations`: Creates Django migration files. Usage: `make makemigrations`
- `superuser`: Creates a superuser for Django admin. Usage: `make superuser`
- `collectstatic`: Collects static files into one location. Usage: `make collectstatic`
- `down-v`: Stops and removes Docker containers and volumes. Usage: `make down-v`
- `volume`: Inspects the volume used by PostgreSQL. Usage: `make volume`
- `estate-db`: Accesses the PostgreSQL database shell. Usage: `make estate-db`
- `test`: Runs tests using pytest with coverage. Usage: `make test`
- `test-html`: Runs tests and generates HTML coverage report. Usage: `make test-html`
- `flake8`: Checks Python files for PEP 8 compliance using flake8. Usage: `make flake8`
- `black-check`: Checks Python files for formatting issues using Black. Usage: `make black-check`
- `black-diff`: Shows the diff of formatting changes using Black. Usage: `make black-diff`
- `black`: Formats Python files using Black. Usage: `make black`
- `isort-check`: Checks Python files for import sorting using isort. Usage: `make isort-check`
- `isort-diff`: Shows the diff of import sorting changes using isort. Usage: `make isort-diff`
- `isort`: Sorts imports in Python files using isort. Usage: `make isort`




