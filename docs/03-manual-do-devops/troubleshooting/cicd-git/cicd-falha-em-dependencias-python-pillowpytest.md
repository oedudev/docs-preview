---
id: 168
title: "CI/CD: Falha em dependências Python (Pillow/Pytest)"
updated_at: 2026-01-31T02:22:06.000000Z
---

# CI/CD: Falha em dependências Python (Pillow/Pytest)

# CI/CD: Falha em dependências Python (Pillow/Pytest)

## O Problema
Bibliotecas Python que dependem de compilação C (como `Pillow`, `pytest-cov`, `psycopg2`) falham durante a instalação no pipeline de CI/CD.

## Causa Raiz
O container base (ex: `python:slim` ou `alpine`) não possui as bibliotecas de sistema (libs do OS) necessárias para compilar essas dependências.

## Solução
"Blindar" o Dockerfile instalando as dependências de sistema antes dos pacotes Python.

**Exemplo para Debian/Ubuntu (python:slim):**
```dockerfile
RUN apt-get update && apt-get install -y \
    build-essential \
    libjpeg-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*
```

**Exemplo para Alpine:**
```dockerfile
RUN apk add --no-cache \
    gcc \
    musl-dev \
    jpeg-dev \
    zlib-dev
```