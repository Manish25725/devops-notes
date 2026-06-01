# Maven Wrapper (mvnw) & Multi-Module Maven Projects

![Maven](https://img.shields.io/badge/Maven-Wrapper-blue)
![Java](https://img.shields.io/badge/Java-MultiModule-green)
![DevOps](https://img.shields.io/badge/DevOps-BuildAutomation-orange)
![CI/CD](https://img.shields.io/badge/CI/CD-Enterprise-red)

---

# 📚 Table of Contents

- Introduction
- What is Maven Wrapper?
- Why Maven Wrapper is Important
- Maven Wrapper Files
- Using Maven Wrapper
- Maven Wrapper Workflow
- Benefits of Maven Wrapper
- Multi-Module Maven Projects
- Why Multi-Module Projects are Needed
- Parent POM
- Child Modules
- Aggregator Projects
- Inter-Module Dependencies
- Build Order
- Real-World Example
- Best Practices
- Summary

---

# 📖 Introduction

Large enterprise applications often contain:
- multiple services
- APIs
- shared libraries
- microservices
- frontend/backend modules

Managing them as separate projects becomes difficult.

Maven solves this using:
# 🚀 Multi-Module Projects

At the same time:
- teams may use different Maven versions

To solve version consistency problems:
# 🌟 Maven Wrapper (`mvnw`) is used.

---

# 🧠 What is Maven Wrapper?

> Maven Wrapper allows a project to use a specific Maven version without requiring Maven to be installed globally.

---

# Wrapper Files

When Maven Wrapper is generated:

```text
mvnw
mvnw.cmd
.mvn/
```

files are added.

---

# Platform Support

| File | Platform |
|---|---|
| `mvnw` | Linux/Mac |
| `mvnw.cmd` | Windows |

---

# 🎯 Why Maven Wrapper is Important

Without wrapper:

```text
❌ Developers use different Maven versions
❌ CI/CD servers may fail
❌ Plugin incompatibility
❌ Build inconsistency
```

---

# Maven Wrapper Solves

```text
✔ Consistent Maven version
✔ No manual Maven installation
✔ Easier onboarding
✔ Reliable CI/CD builds
✔ Enterprise standardization
```

---

# 📂 Maven Wrapper Structure

```text
project/
│
├── mvnw
├── mvnw.cmd
├── .mvn/
│   └── wrapper/
│       └── maven-wrapper.properties
│
└── pom.xml
```

---

# ⚙️ How Maven Wrapper Works

---

# Developer Runs

Linux/Mac:

```bash
./mvnw clean package
```

Windows:

```cmd
mvnw.cmd clean package
```

---

# Maven Wrapper Automatically

```text
✔ Downloads required Maven version
✔ Uses configured version
✔ Executes build
```

---

# 🌟 Maven Wrapper Configuration

Inside:

```text
.mvn/wrapper/maven-wrapper.properties
```

---

# Example

```properties
distributionUrl=https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.9.6/apache-maven-3.9.6-bin.zip
```

---

# Result

Project always uses:
```text
Maven 3.9.6
```

---

# 🛠️ Generating Maven Wrapper

---

# Command

```bash
mvn -N wrapper:wrapper
```

---

# Result

Creates:
```text
✔ mvnw
✔ mvnw.cmd
✔ .mvn folder
```

---

# 🌍 Real-World Usage

CI/CD pipelines use:

```bash
./mvnw clean package
```

instead of:

```bash
mvn clean package
```

---

# Why?

Ensures:
- same Maven version everywhere

---

# 🧠 What are Multi-Module Maven Projects?

> Multi-Module Projects allow multiple Maven projects/modules to be managed together using a parent project.

---

# Example Enterprise Structure

```text
banking-system/
│
├── pom.xml
│
├── common-library/
├── user-service/
├── payment-service/
├── notification-service/
└── api-gateway/
```

---

# Each Module

```text
✔ Independent
✔ Reusable
✔ Buildable separately
✔ Managed together
```

---

# 🎯 Why Multi-Module Projects are Needed

Large projects become difficult if:
- everything inside one module

---

# Problems with Single Large Project

```text
❌ Hard maintenance
❌ Slow builds
❌ Tight coupling
❌ Difficult testing
❌ Poor scalability
```

---

# Multi-Module Benefits

```text
✔ Better organization
✔ Faster builds
✔ Reusable modules
✔ Easier collaboration
✔ Independent deployment
✔ Microservices support
```

---

# 📦 Parent POM

Main project contains:
- Parent POM

---

# Responsibilities

```text
✔ Shared dependency versions
✔ Shared plugins
✔ Shared configuration
✔ Module definitions
```

---

# Parent POM Packaging

```xml
<packaging>pom</packaging>
```

---

# Example Parent POM

```xml
<project>

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.company</groupId>

    <artifactId>banking-system</artifactId>

    <version>1.0.0</version>

    <packaging>pom</packaging>

    <modules>

        <module>common-library</module>

        <module>user-service</module>

        <module>payment-service</module>

    </modules>

</project>
```

---

# 🧩 Child Modules

Each module has:
- its own POM.xml

---

# Example Child Module

```xml
<project>

    <parent>

        <groupId>com.company</groupId>

        <artifactId>banking-system</artifactId>

        <version>1.0.0</version>

    </parent>

    <artifactId>user-service</artifactId>

</project>
```

---

# Result

Child module inherits:
```text
✔ Dependency versions
✔ Plugin configuration
✔ Build settings
```

---

# 🌟 Aggregator Project

Parent project acts as:
# Aggregator

---

# Purpose

Build all modules together.

---

# Command

```bash
mvn clean install
```

---

# Maven Automatically

```text
✔ Builds common-library
✔ Builds user-service
✔ Builds payment-service
✔ Resolves dependencies
```

---

# 🔄 Inter-Module Dependencies

One module may depend on another.

---

# Example

```text
user-service
      ↓
common-library
```

---

# Dependency Example

```xml
<dependency>

    <groupId>com.company</groupId>

    <artifactId>common-library</artifactId>

    <version>1.0.0</version>

</dependency>
```

---

# Maven Automatically

```text
✔ Builds common-library first
✔ Then builds user-service
```

---

# 🏗️ Build Order in Multi-Module Projects

Maven automatically determines:
- correct build order

based on:
- dependencies

---

# Example

```text
common-library
      ↓
payment-service
      ↓
api-gateway
```

---

# Build Order

```text
1. common-library
2. payment-service
3. api-gateway
```

---

# 🌍 Real-World Enterprise Example

---

# E-Commerce Platform

```text
ecommerce-system/
│
├── common-utils/
├── product-service/
├── order-service/
├── payment-service/
├── inventory-service/
└── api-gateway/
```

---

# Benefits

```text
✔ Independent services
✔ Shared utilities
✔ Faster deployment
✔ Easier scaling
✔ Microservice architecture support
```

---

# 🚀 Multi-Module Build Workflow

```text
Parent POM
      ↓
Identify Modules
      ↓
Resolve Dependencies
      ↓
Build in Correct Order
      ↓
Generate Artifacts
```

---

# 🛠️ Useful Maven Wrapper Commands

| Command | Purpose |
|---|---|
| `./mvnw clean` | Clean project |
| `./mvnw compile` | Compile project |
| `./mvnw test` | Run tests |
| `./mvnw package` | Create JAR/WAR |
| `./mvnw install` | Install locally |

---

# 🛠️ Useful Multi-Module Commands

| Command | Purpose |
|---|---|
| `mvn clean install` | Build all modules |
| `mvn -pl module-name install` | Build specific module |
| `mvn dependency:tree` | View dependencies |
| `mvn help:effective-pom` | View final POM |

---

# 🔐 Best Practices

---

# Always Use Maven Wrapper

Especially in:
- teams
- CI/CD pipelines

---

# Keep Parent POM Clean

Avoid unnecessary dependencies.

---

# Use Dependency Management

Centralize versions.

---

# Separate Shared Libraries

Create:
```text
common-utils module
```

---

# Avoid Circular Dependencies

Bad architecture causes:
- build failures

---

# Use Semantic Versioning

```text
1.0.0
1.1.0
2.0.0
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Maven Wrapper | Project-specific Maven version |
| mvnw | Wrapper script |
| Parent POM | Shared project configuration |
| Module | Subproject |
| Aggregator | Builds all modules |
| Multi-Module Project | Collection of Maven modules |

---

# 🧠 Important Keywords

- Maven Wrapper
- mvnw
- Parent POM
- Child Module
- Multi-Module Project
- Aggregator
- Inter-Module Dependency
- Build Order
- CI/CD
- Enterprise Architecture

---

# ❓ Viva Questions

1. What is Maven Wrapper?
2. Why use mvnw?
3. What is Parent POM?
4. What is multi-module project?
5. What is aggregator project?
6. Why use multi-module architecture?
7. What is inter-module dependency?
8. How does Maven determine build order?
9. Difference between parent and child POM?
10. Why use Maven Wrapper in CI/CD?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is Maven Wrapper? | Project-specific Maven execution |
| Why use mvnw instead of mvn? | Version consistency |
| What is Parent POM? | Shared configuration POM |
| What is multi-module project? | Multiple Maven projects managed together |
| What is aggregator POM? | Builds all modules together |

---

# 🌟 Important Interview Scenario

## Question

Why is Maven Wrapper important in enterprise CI/CD pipelines?

## Answer

Maven Wrapper ensures:
- same Maven version across:
  - developers
  - CI/CD servers
  - production builds

This avoids:
- version mismatch
- plugin incompatibility
- inconsistent builds

---

# ✅ Conclusion

Maven Wrapper and Multi-Module Projects are essential for:
- enterprise Java applications
- microservices
- CI/CD pipelines
- scalable development

Using:
- Parent POMs
- child modules
- wrappers
- centralized configuration

organizations achieve:
```text
✔ Consistency
✔ Scalability
✔ Reusability
✔ Faster builds
✔ Better collaboration
✔ Enterprise-grade architecture
```

These concepts are heavily used in:
- Spring Boot
- Microservices
- Kubernetes deployments
- DevOps pipelines
- Cloud-native applications