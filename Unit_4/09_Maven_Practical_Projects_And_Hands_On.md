# Maven Practical Projects & Hands-On Labs

![Maven](https://img.shields.io/badge/Maven-PracticalLabs-blue)
![Java](https://img.shields.io/badge/Java-Projects-green)
![Docker](https://img.shields.io/badge/Docker-Integration-orange)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-red)

---

# 📚 Table of Contents

- Introduction
- Project 1 — Basic Maven Java Application
- Project 2 — Maven + JUnit Testing
- Project 3 — Maven Web Application
- Project 4 — Spring Boot Maven Project
- Project 5 — Multi-Module Maven Project
- Project 6 — Maven + Docker Integration
- Project 7 — Maven + GHCR Deployment
- CI/CD Workflow Example
- Common Errors & Fixes
- Best Practices
- Summary

---

# 📖 Introduction

Practical projects help understand:
- Maven lifecycle
- dependencies
- plugins
- testing
- Docker integration
- CI/CD pipelines

This file contains:
```text
✔ Hands-on labs
✔ Real-world Maven projects
✔ Docker integration
✔ Registry deployment
✔ CI/CD workflows
```

---

# 🚀 Project 1 — Basic Maven Java Application

---

# 🎯 Goal

Create:
- simple Java Maven application

---

# Step 1 — Create Project

```bash
mvn archetype:generate
```

---

# Maven Asks

```text
groupId: com.example
artifactId: demo-app
version: 1.0.0
```

---

# Generated Structure

```text
demo-app/
│
├── pom.xml
├── src/
│   ├── main/java
│   └── test/java
```

---

# Step 2 — Add Java Code

## File

```text
src/main/java/com/example/App.java
```

---

# Code

```java
package com.example;

public class App {

    public static void main(String[] args) {

        System.out.println("Hello Maven!");

    }

}
```

---

# Step 3 — Compile Project

```bash
mvn compile
```

---

# Step 4 — Run Project

```bash
mvn exec:java -Dexec.mainClass="com.example.App"
```

---

# Output

```text
Hello Maven!
```

---

# 🌟 Concepts Learned

```text
✔ Maven structure
✔ Compile phase
✔ Java execution
✔ Build automation
```

---

# 🧪 Project 2 — Maven + JUnit Testing

---

# 🎯 Goal

Run unit tests using:
- Maven Surefire Plugin

---

# Step 1 — Add JUnit Dependency

```xml
<dependency>

    <groupId>junit</groupId>

    <artifactId>junit</artifactId>

    <version>4.13.2</version>

    <scope>test</scope>

</dependency>
```

---

# Step 2 — Create Test Class

## File

```text
src/test/java/com/example/AppTest.java
```

---

# Code

```java
package com.example;

import org.junit.Test;

import static org.junit.Assert.*;

public class AppTest {

    @Test
    public void testAddition() {

        assertEquals(4, 2 + 2);

    }

}
```

---

# Step 3 — Run Tests

```bash
mvn test
```

---

# Result

```text
✔ Tests executed
✔ Reports generated
✔ Build successful
```

---

# 🌟 Concepts Learned

```text
✔ Test scope
✔ Surefire plugin
✔ Unit testing
✔ Test automation
```

---

# 🌐 Project 3 — Maven Web Application

---

# 🎯 Goal

Create:
- simple Java web application

---

# Step 1 — Create Web App

```bash
mvn archetype:generate
```

Choose:
```text
maven-archetype-webapp
```

---

# Project Structure

```text
web-app/
│
├── pom.xml
├── src/main/webapp
│   └── index.jsp
```

---

# Step 2 — Add JSP

## File

```text
index.jsp
```

---

# Code

```jsp
<html>

<body>

<h1>Hello Maven Web App</h1>

</body>

</html>
```

---

# Step 3 — Package WAR

```bash
mvn package
```

---

# Output

```text
target/web-app.war
```

---

# Step 4 — Deploy to Tomcat

Copy:
```text
web-app.war
```

to:
```text
webapps/
```

folder.

---

# 🌟 Concepts Learned

```text
✔ WAR packaging
✔ Web application structure
✔ Deployment
✔ Servlet containers
```

---

# 🌱 Project 4 — Spring Boot Maven Project

---

# 🎯 Goal

Create:
- REST API using Spring Boot + Maven

---

# Step 1 — Create pom.xml

```xml
<project>

    <parent>

        <groupId>org.springframework.boot</groupId>

        <artifactId>spring-boot-starter-parent</artifactId>

        <version>3.2.0</version>

    </parent>

    <dependencies>

        <dependency>

            <groupId>org.springframework.boot</groupId>

            <artifactId>spring-boot-starter-web</artifactId>

        </dependency>

    </dependencies>

</project>
```

---

# Step 2 — Create Main Class

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {

        SpringApplication.run(DemoApplication.class, args);

    }

}
```

---

# Step 3 — Create Controller

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/")

    public String hello() {

        return "Hello Spring Boot Maven!";

    }

}
```

---

# Step 4 — Run Application

```bash
mvn spring-boot:run
```

---

# Access

```text
http://localhost:8080
```

---

# 🌟 Concepts Learned

```text
✔ Spring Boot
✔ REST API
✔ Maven plugins
✔ Dependency management
```

---

# 🧩 Project 5 — Multi-Module Maven Project

---

# 🎯 Goal

Create:
- parent project
- multiple modules

---

# Structure

```text
banking-system/
│
├── pom.xml
├── common-library/
├── user-service/
└── payment-service/
```

---

# Parent POM

```xml
<packaging>pom</packaging>

<modules>

    <module>common-library</module>

    <module>user-service</module>

</modules>
```

---

# Build All Modules

```bash
mvn clean install
```

---

# Result

```text
✔ All modules compiled
✔ Dependencies resolved
✔ Artifacts generated
```

---

# 🌟 Concepts Learned

```text
✔ Parent POM
✔ Child modules
✔ Aggregator projects
✔ Enterprise architecture
```

---

# 🐳 Project 6 — Maven + Docker Integration

---

# 🎯 Goal

Dockerize Maven-based Java application.

---

# Step 1 — Build JAR

```bash
mvn clean package
```

---

# Output

```text
target/demo.jar
```

---

# Step 2 — Create Dockerfile

```dockerfile
FROM eclipse-temurin:17

WORKDIR /app

COPY target/demo.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```

---

# Step 3 — Build Docker Image

```bash
docker build -t demo-app:v1 .
```

---

# Step 4 — Run Container

```bash
docker run -p 8080:8080 demo-app:v1
```

---

# 🌟 Concepts Learned

```text
✔ Docker integration
✔ Containerization
✔ JAR deployment
✔ Cloud-native apps
```

---

# 🌍 Project 7 — Maven + GHCR Deployment

---

# 🎯 Goal

Push Dockerized Maven app to:
- GitHub Container Registry

---

# Step 1 — Login to GHCR

```bash
docker login ghcr.io
```

---

# Step 2 — Tag Image

```bash
docker tag demo-app:v1 ghcr.io/komaljoshi17/demo-app:v1
```

---

# Step 3 — Push Image

```bash
docker push ghcr.io/komaljoshi17/demo-app:v1
```

---

# Step 4 — Pull Image

```bash
docker pull ghcr.io/komaljoshi17/demo-app:v1
```

---

# 🌟 Concepts Learned

```text
✔ Container registries
✔ GHCR
✔ Image distribution
✔ CI/CD readiness
```

---

# 🚀 CI/CD Workflow Example

---

# GitHub Actions Workflow

```yaml
name: Maven CI

on: [push]

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v3

      - name: Setup Java
        uses: actions/setup-java@v3
        with:
          distribution: temurin
          java-version: 17

      - name: Build Project
        run: mvn clean package

      - name: Build Docker Image
        run: docker build -t app:v1 .

      - name: Push Image
        run: docker push app:v1
```

---

# Workflow

```text
Git Push
    ↓
Maven Build
    ↓
Tests
    ↓
Docker Build
    ↓
Registry Push
    ↓
Deployment
```

---

# ⚠️ Common Errors & Fixes

| Error | Cause | Solution |
|---|---|---|
| Dependency not found | Wrong version | Check Maven Central |
| Build failure | Java mismatch | Verify JDK version |
| Plugin error | Missing plugin | Add plugin version |
| Docker build fails | Missing JAR | Run mvn package |
| Port conflict | Port already used | Change port |

---

# 🛠️ Useful Commands

| Command | Purpose |
|---|---|
| `mvn compile` | Compile source |
| `mvn test` | Run tests |
| `mvn package` | Create JAR/WAR |
| `mvn install` | Install locally |
| `docker build` | Create image |
| `docker run` | Run container |

---

# 🔐 Best Practices

---

# Use Maven Wrapper

```bash
./mvnw clean package
```

---

# Keep Dependencies Updated

Avoid:
```text
vulnerable libraries
```

---

# Use Multi-Stage Docker Builds

Smaller image sizes.

---

# Always Run Tests

```bash
mvn test
```

before deployment.

---

# Use Semantic Versioning

```text
1.0.0
1.1.0
2.0.0
```

---

# 📊 Maven + Docker Workflow Diagram

```text
Source Code
     ↓
Maven Build
     ↓
JAR/WAR
     ↓
Docker Build
     ↓
Registry Push
     ↓
Deployment
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Maven | Build automation tool |
| JAR | Java archive |
| WAR | Web archive |
| Docker | Container platform |
| GHCR | GitHub Container Registry |
| Multi-module | Multiple Maven projects |

---

# 🧠 Important Keywords

- Maven
- Spring Boot
- Docker
- GHCR
- JUnit
- Multi-module
- CI/CD
- Maven Wrapper
- REST API
- Dockerfile

---

# ❓ Viva Questions

1. How do you create a Maven project?
2. What is mvn package?
3. Difference between JAR and WAR?
4. How do you run tests in Maven?
5. How does Maven integrate with Docker?
6. What is GHCR?
7. What is Spring Boot starter?
8. Why use Maven Wrapper?
9. What is multi-module architecture?
10. Why use Docker with Maven?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| How do you build Maven project? | mvn clean package |
| How do you Dockerize Maven app? | Build JAR + Dockerfile |
| What is Spring Boot starter? | Preconfigured dependency bundle |
| Why use multi-module projects? | Better scalability |
| What is GHCR? | GitHub Container Registry |

---

# ✅ Conclusion

These practical Maven projects provide:
```text
✔ Real-world development experience
✔ Build automation knowledge
✔ Docker integration
✔ CI/CD understanding
✔ Enterprise project structure
```

By completing these projects, students learn:
- Maven lifecycle
- dependency management
- plugin execution
- Spring Boot
- Docker integration
- registry deployment
- DevOps workflows

These skills are essential for:
```text
✔ Java Development
✔ Backend Engineering
✔ DevOps
✔ Cloud Computing
✔ Microservices
✔ Enterprise Software Development
```