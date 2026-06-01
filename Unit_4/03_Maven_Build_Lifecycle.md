# Maven Build Lifecycle

![Maven](https://img.shields.io/badge/Maven-BuildLifecycle-blue)
![Java](https://img.shields.io/badge/Java-Automation-green)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-orange)
![Build](https://img.shields.io/badge/Build-Phases-red)

---

# 📚 Table of Contents

- Introduction
- What is Maven Build Lifecycle?
- Why Lifecycle is Important
- Maven Lifecycles
- Default Lifecycle
- Clean Lifecycle
- Site Lifecycle
- Build Lifecycle Phases
- validate
- compile
- test
- package
- verify
- install
- deploy
- Lifecycle Workflow
- Maven Commands
- Real-World Examples
- Best Practices
- Summary

---

# 📖 Introduction

Building a software project involves multiple steps:

```text
✔ Validate project
✔ Compile code
✔ Run tests
✔ Package application
✔ Install artifact
✔ Deploy application
```

Doing these manually is:
- difficult
- repetitive
- error-prone

Maven automates this process using:
# 🚀 Build Lifecycle

---

# 🧠 What is Maven Build Lifecycle?

> Maven Build Lifecycle is a predefined sequence of phases used to build and manage a project automatically.

---

# Example Workflow

```text
Source Code
    ↓
Compile
    ↓
Test
    ↓
Package
    ↓
Install
    ↓
Deploy
```

---

# Purpose

```text
✔ Standardized build process
✔ Automation
✔ Consistency
✔ CI/CD integration
✔ Faster development
```

---

# 🎯 Why Lifecycle is Important

Without lifecycle:

```text
❌ Manual builds
❌ Missing steps
❌ Deployment errors
❌ Inconsistent packaging
❌ Testing skipped accidentally
```

---

# Maven Lifecycle Solves

```text
✔ Automatic workflow
✔ Correct execution order
✔ Reliable builds
✔ Better productivity
✔ Enterprise-grade automation
```

---

# 🔄 Maven Lifecycles

Maven has three built-in lifecycles.

---

# Main Lifecycles

| Lifecycle | Purpose |
|---|---|
| Default | Build & deployment |
| Clean | Remove old build files |
| Site | Generate project documentation |

---

# 🌟 1. Default Lifecycle

Main lifecycle used for:
- building applications

---

# Includes Phases

```text
validate
compile
test
package
verify
install
deploy
```

---

# Most Common Lifecycle

Used in:
- Java projects
- Spring Boot
- Enterprise applications
- CI/CD pipelines

---

# 🧹 2. Clean Lifecycle

Used to:
- remove previous build files

---

# Command

```bash
mvn clean
```

---

# Removes

```text
target/
```

folder.

---

# Why Important?

Avoids:
- old compiled files
- corrupted builds
- stale artifacts

---

# 📄 3. Site Lifecycle

Used to generate:
- project documentation
- reports
- dependency analysis

---

# Command

```bash
mvn site
```

---

# Output

```text
target/site/
```

---

# 🏗️ Maven Build Lifecycle Phases

The Default Lifecycle contains several phases.

---

# Execution Order

```text
validate
   ↓
compile
   ↓
test
   ↓
package
   ↓
verify
   ↓
install
   ↓
deploy
```

---

# Important Rule

Running a later phase automatically executes:
- all previous phases

---

# Example

```bash
mvn package
```

Automatically runs:

```text
validate → compile → test → package
```

---

# 📌 Phase 1 — validate

---

# Purpose

Checks:
- project correctness
- required information

---

# Validates

```text
✔ pom.xml exists
✔ dependencies available
✔ project structure valid
```

---

# Command

```bash
mvn validate
```

---

# 📌 Phase 2 — compile

---

# Purpose

Compiles:
- Java source code

---

# Input

```text
src/main/java
```

---

# Output

```text
target/classes
```

---

# Command

```bash
mvn compile
```

---

# Result

```text
✔ .java → .class conversion
✔ Source code compiled
```

---

# 📌 Phase 3 — test

---

# Purpose

Runs:
- unit tests

using testing frameworks like:
- JUnit
- TestNG

---

# Input

```text
src/test/java
```

---

# Command

```bash
mvn test
```

---

# Result

```text
✔ Unit tests executed
✔ Reports generated
✔ Build fails if tests fail
```

---

# Example

```java
@Test
public void testAddition() {
    assertEquals(4, 2 + 2);
}
```

---

# 📌 Phase 4 — package

---

# Purpose

Packages compiled code into:
- JAR
- WAR

---

# Output Location

```text
target/
```

---

# Command

```bash
mvn package
```

---

# Example Output

```text
target/myapp-1.0.0.jar
```

---

# Result

```text
✔ Deployable artifact created
✔ Application packaged
```

---

# 📌 Phase 5 — verify

---

# Purpose

Performs:
- quality checks
- integration checks
- validation

---

# Example

```text
✔ Integration testing
✔ Code quality analysis
✔ Security scanning
```

---

# Command

```bash
mvn verify
```

---

# 📌 Phase 6 — install

---

# Purpose

Installs built artifact into:
- local Maven repository

---

# Local Repository

```text
~/.m2/repository
```

---

# Command

```bash
mvn install
```

---

# Result

```text
✔ Artifact available locally
✔ Other projects can use it
```

---

# Example

Another project can now use:

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>myapp</artifactId>
    <version>1.0.0</version>
</dependency>
```

---

# 📌 Phase 7 — deploy

---

# Purpose

Uploads artifact to:
- remote repository

---

# Example Repositories

```text
✔ Nexus
✔ Artifactory
✔ GitHub Packages
✔ Maven Central
```

---

# Command

```bash
mvn deploy
```

---

# Result

```text
✔ Artifact shared globally
✔ CI/CD deployment enabled
```

---

# 📊 Lifecycle Workflow Diagram

```text
validate
   ↓
compile
   ↓
test
   ↓
package
   ↓
verify
   ↓
install
   ↓
deploy
```

---

# 🛠️ Common Maven Lifecycle Commands

| Command | Purpose |
|---|---|
| `mvn clean` | Remove old build |
| `mvn compile` | Compile code |
| `mvn test` | Run tests |
| `mvn package` | Create JAR/WAR |
| `mvn verify` | Verify quality |
| `mvn install` | Install locally |
| `mvn deploy` | Upload remotely |

---

# 🌟 Real-World Example

---

# Spring Boot Build

```bash
mvn clean package
```

---

# Maven Automatically

```text
✔ Cleans target folder
✔ Downloads dependencies
✔ Compiles code
✔ Runs tests
✔ Creates executable JAR
```

---

# Output

```text
target/spring-app.jar
```

---

# Docker Integration

After Maven package:

```bash
docker build -t spring-app:v1 .
```

---

# CI/CD Pipeline Example

```text
Git Push
   ↓
Jenkins
   ↓
mvn clean package
   ↓
Docker Build
   ↓
Kubernetes Deploy
```

---

# 🔐 Best Practices

---

# Always Run Clean Before Package

✅ Good

```bash
mvn clean package
```

---

# Use install for Local Development

Allows:
- local dependency sharing

---

# Use deploy in CI/CD Only

Avoid unnecessary remote uploads.

---

# Keep Tests Fast

Slow tests:
- delay pipeline

---

# Use verify for Quality Gates

Include:
- security scanning
- integration testing

---

# 📌 Quick Revision Notes

| Phase | Purpose |
|---|---|
| validate | Check project correctness |
| compile | Compile Java code |
| test | Run unit tests |
| package | Create JAR/WAR |
| verify | Quality checks |
| install | Install locally |
| deploy | Upload remotely |

---

# 🧠 Important Keywords

- Build Lifecycle
- validate
- compile
- test
- package
- verify
- install
- deploy
- Artifact
- Maven Repository

---

# ❓ Viva Questions

1. What is Maven lifecycle?
2. What are Maven lifecycles?
3. What is compile phase?
4. What happens in package phase?
5. Difference between install and deploy?
6. What does mvn clean do?
7. What is target folder?
8. Why is test phase important?
9. What is verify phase?
10. Why use Maven lifecycle?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is Maven build lifecycle? | Predefined build workflow |
| Difference between package and install? | Local repo installation |
| Difference between install and deploy? | Local vs remote repository |
| What does mvn clean package do? | Clean + full build |
| Why use Maven lifecycle? | Build automation |

---

# 🌟 Important Interview Scenario

## Question

What happens when you run:

```bash
mvn package
```

## Answer

Maven automatically executes:

```text
validate
compile
test
package
```

in sequence and generates:
- deployable JAR/WAR artifact.

---

# ✅ Conclusion

Maven Build Lifecycle automates:
- compilation
- testing
- packaging
- deployment

Using:
- predefined phases
- standardized workflows
- automation

Maven enables:
- reliable builds
- CI/CD pipelines
- scalable Java development
- enterprise-grade deployment systems

Understanding lifecycle phases is essential for:
- Spring Boot
- DevOps
- CI/CD
- Docker integration
- Kubernetes deployments