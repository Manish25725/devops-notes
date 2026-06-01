# GitHub Marketplace Actions & Caching

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![Marketplace](https://img.shields.io/badge/Marketplace-Actions-blue)
![Caching](https://img.shields.io/badge/Caching-Build_Optimization-green)
![DevOps](https://img.shields.io/badge/DevOps-CI_CD-orange)

---

# 📚 Table of Contents

- Introduction
- What is GitHub Marketplace?
- Why Marketplace Actions Exist
- Benefits of Marketplace Actions
- Popular Marketplace Actions
- Language-Specific Actions
- What is Caching?
- Why Caching is Important
- Maven Dependency Caching
- Node.js Dependency Caching
- Python Dependency Caching
- Docker Layer Caching
- Cache Keys
- Cache Hit vs Cache Miss
- Best Practices
- Quick Revision
- Viva Questions
- Interview Questions

---

# Introduction

In modern CI/CD pipelines:

```text
Build
↓
Test
↓
Deploy
```

many tasks are repeated.

Examples:

- Installing Java
- Installing Node.js
- Downloading Maven dependencies
- Downloading npm packages
- Downloading Python libraries

Doing this every workflow run wastes time.

GitHub solves this using:

```text
Marketplace Actions
```

and

```text
Caching
```

---

# What is GitHub Marketplace?

GitHub Marketplace is a collection of reusable Actions created by:

- GitHub
- Organizations
- Open Source Contributors
- Companies

These actions simplify workflow creation.

---

# Marketplace Website

:contentReference[oaicite:0]{index=0}

---

# Why Marketplace Actions Exist?

Without Actions:

```yaml
run: |
  git clone ...
  install java ...
  configure environment ...
```

Large amount of code.

---

With Actions:

```yaml
uses: actions/checkout@v4
```

Done instantly.

---

# Marketplace Concept

```text
Developer
      ↓
Uses Action
      ↓
Action Performs Work
      ↓
Workflow Continues
```

---

# Benefits of Marketplace Actions

| Benefit | Description |
|----------|----------|
| Reusable | Write once, use everywhere |
| Faster Setup | Less YAML code |
| Community Support | Maintained by experts |
| Reliability | Tested and verified |
| Productivity | Faster CI/CD development |

---

# Popular Marketplace Actions

| Action | Purpose |
|----------|----------|
| actions/checkout | Clone repository |
| actions/setup-java | Install Java |
| actions/setup-node | Install Node.js |
| actions/setup-python | Install Python |
| actions/cache | Cache dependencies |
| docker/login-action | Docker Login |
| docker/build-push-action | Docker Build & Push |
| upload-artifact | Upload build files |
| download-artifact | Download build files |

---

# 1. Checkout Action

Most workflows start by downloading source code.

---

## Example

```yaml
- name: Checkout Repository

  uses: actions/checkout@v4
```

---

## What It Does

```text
Repository
      ↓
Clone
      ↓
Runner Workspace
```

---

# 2. Setup Java Action

Used in Java/Maven projects.

---

## Example

```yaml
- name: Setup Java

  uses: actions/setup-java@v4

  with:

    distribution: temurin

    java-version: 21
```

---

# Result

```text
Java Installed
JAVA_HOME Configured
Ready for Maven Build
```

---

# 3. Setup Node Action

Used in JavaScript projects.

---

## Example

```yaml
- name: Setup Node

  uses: actions/setup-node@v4

  with:

    node-version: 20
```

---

# Result

```text
Node Installed
npm Available
Ready for Build
```

---

# 4. Setup Python Action

Used in Python projects.

---

## Example

```yaml
- uses: actions/setup-python@v5

  with:

    python-version: "3.12"
```

---

# Result

```text
Python Installed
pip Available
Ready for Execution
```

---

# Language-Specific Actions

| Language | Action |
|----------|----------|
| Java | setup-java |
| Node.js | setup-node |
| Python | setup-python |
| Go | setup-go |
| .NET | setup-dotnet |
| Ruby | setup-ruby |

---

# Example Java Workflow

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: actions/setup-java@v4

    with:

      distribution: temurin

      java-version: 21

  - run: mvn clean package
```

---

# Example Node.js Workflow

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: actions/setup-node@v4

    with:

      node-version: 20

  - run: npm install

  - run: npm test
```

---

# What is Caching?

Caching stores downloaded files between workflow runs.

Instead of downloading again:

```text
Use Saved Copy
```

---

# Why Caching is Important?

Without Cache:

```text
Workflow Start
      ↓
Download Dependencies
      ↓
Build
```

Every run downloads again.

Slow.

---

# With Cache

```text
Workflow Start
      ↓
Use Cached Files
      ↓
Build
```

Much faster.

---

# Build Time Comparison

| Scenario | Build Time |
|-----------|-----------|
| No Cache | 5-10 min |
| Cache Hit | 30 sec - 2 min |

---

# Caching Architecture

```text
First Build
      ↓
Download Dependencies
      ↓
Store Cache

Future Builds
      ↓
Restore Cache
      ↓
Build Faster
```

---

# Maven Dependency Caching

Maven stores dependencies in:

```text
~/.m2/repository
```

Downloading every build is slow.

---

# Maven Cache Example

```yaml
- uses: actions/cache@v4

  with:

    path: ~/.m2/repository

    key: maven-${{ hashFiles('pom.xml') }}
```

---

# Flow

```text
pom.xml
      ↓
Generate Key
      ↓
Save Cache
      ↓
Reuse Later
```

---

# Complete Maven Example

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: actions/setup-java@v4

    with:

      distribution: temurin

      java-version: 21

  - uses: actions/cache@v4

    with:

      path: ~/.m2/repository

      key: maven-${{ hashFiles('pom.xml') }}

  - run: mvn clean package
```

---

# Node.js Dependency Caching

Node packages stored in:

```text
node_modules
```

or

```text
npm cache
```

---

# Example

```yaml
- uses: actions/cache@v4

  with:

    path: ~/.npm

    key: npm-${{ hashFiles('package-lock.json') }}
```

---

# Node Workflow Example

```yaml
steps:

  - uses: actions/setup-node@v4

    with:

      node-version: 20

  - uses: actions/cache@v4

    with:

      path: ~/.npm

      key: npm-${{ hashFiles('package-lock.json') }}

  - run: npm install

  - run: npm test
```

---

# Python Dependency Caching

Python packages stored in:

```text
~/.cache/pip
```

---

# Example

```yaml
- uses: actions/cache@v4

  with:

    path: ~/.cache/pip

    key: pip-${{ hashFiles('requirements.txt') }}
```

---

# Docker Layer Caching

Docker images use layers.

Layers can also be cached.

---

# Example

```yaml
- uses: docker/build-push-action@v6

  with:

    cache-from: type=gha

    cache-to: type=gha,mode=max
```

---

# Benefits

```text
Faster Docker Builds
Reduced Downloads
Less Network Usage
```

---

# What is a Cache Key?

A cache key uniquely identifies cache contents.

---

# Example

```yaml
key: maven-${{ hashFiles('pom.xml') }}
```

---

# Why Use hashFiles?

If dependencies change:

```text
pom.xml Updated
      ↓
New Hash
      ↓
New Cache Created
```

---

# Cache Hit vs Cache Miss

---

## Cache Hit

```text
Cache Found
      ↓
Restore Files
      ↓
Fast Build
```

---

## Cache Miss

```text
No Cache
      ↓
Download Everything
      ↓
Create Cache
```

---

# Visualization

```text
Workflow

      ↓

Cache Exists?

   YES      NO

    ↓        ↓

 Restore   Download

    ↓        ↓

 Build     Build

    ↓        ↓

 Fast     Slow
```

---

# Complete Cached Maven Workflow

```yaml
name: Maven CI

on:

  push:

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4

        with:

          distribution: temurin

          java-version: 21

      - uses: actions/cache@v4

        with:

          path: ~/.m2/repository

          key: maven-${{ hashFiles('pom.xml') }}

      - run: mvn clean package
```

---

# Best Practices

✔ Cache dependencies

✔ Use hashFiles()

✔ Keep cache keys unique

✔ Use official actions

✔ Use latest action versions

✔ Avoid caching build outputs

✔ Cache package managers only

---

# Quick Revision Notes

## Marketplace

```text
Reusable Actions
```

---

## setup-java

```text
Install Java
```

---

## setup-node

```text
Install Node.js
```

---

## setup-python

```text
Install Python
```

---

## Cache

```text
Store dependencies
```

---

## Cache Key

```text
Unique cache identifier
```

---

# Frequently Used Actions

| Action | Purpose |
|----------|----------|
| checkout | Clone Repo |
| setup-java | Java Setup |
| setup-node | Node Setup |
| setup-python | Python Setup |
| cache | Speed Up Builds |

---

# Viva Questions

### 1. What is GitHub Marketplace?

A repository of reusable GitHub Actions.

---

### 2. Why use Marketplace Actions?

To simplify workflow development.

---

### 3. What does actions/checkout do?

Clones repository source code.

---

### 4. What does setup-java do?

Installs Java on runner.

---

### 5. Why use caching?

To reduce build time.

---

### 6. What is a cache key?

Unique identifier for cache data.

---

### 7. What is a cache hit?

Previously saved cache found.

---

### 8. What is a cache miss?

No cache found; dependencies downloaded again.

---

# Interview Questions

## Q1. Explain caching in GitHub Actions.

Caching stores dependencies between workflow runs to reduce build time.

---

## Q2. Why cache Maven dependencies?

Maven downloads many libraries. Caching avoids repeated downloads.

---

## Q3. Difference between cache hit and cache miss?

Cache Hit:

```text
Cache restored
```

Cache Miss:

```text
Dependencies downloaded
```

---

## Q4. What is hashFiles() used for?

Generating cache keys based on file changes.

---

## Q5. Name three official GitHub Actions.

- actions/checkout
- actions/setup-java
- actions/cache

---

# Key Terms

| Term | Meaning |
|---------|---------|
| Marketplace | Action repository |
| Action | Reusable automation |
| Cache | Stored dependency data |
| Cache Key | Cache identifier |
| Cache Hit | Cache found |
| Cache Miss | Cache not found |

---

# Summary

GitHub Marketplace provides reusable Actions that simplify CI/CD workflows.

Popular actions include:

✔ checkout

✔ setup-java

✔ setup-node

✔ setup-python

✔ cache

Caching significantly improves performance by storing dependencies between workflow runs, reducing build times and improving CI/CD efficiency.