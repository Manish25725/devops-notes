# Maven Plugins & Plugin Execution

![Maven](https://img.shields.io/badge/Maven-Plugins-blue)
![Java](https://img.shields.io/badge/Java-BuildTools-green)
![DevOps](https://img.shields.io/badge/DevOps-Automation-orange)
![Plugins](https://img.shields.io/badge/Plugins-Execution-red)

---

# 📚 Table of Contents

- Introduction
- What are Maven Plugins?
- Why Plugins are Important
- Plugin Architecture
- Plugin Goals
- Plugin Execution
- Build Plugins vs Reporting Plugins
- Maven Compiler Plugin
- Maven Surefire Plugin
- Maven Shade Plugin
- Maven Jar Plugin
- Maven Clean Plugin
- Maven Resources Plugin
- Plugin Configuration
- Maven Wrapper (mvnw)
- Real-World Examples
- Best Practices
- Summary

---

# 📖 Introduction

Maven itself provides:
- lifecycle phases

But actual tasks like:
- compiling Java code
- running tests
- packaging JARs

are performed using:
# 🔌 Maven Plugins

---

# 🧠 What are Maven Plugins?

> Maven Plugins are reusable components that perform specific tasks during the Maven build lifecycle.

---

# Examples

```text
✔ Compile Java code
✔ Run unit tests
✔ Create executable JARs
✔ Generate reports
✔ Build Docker images
✔ Deploy applications
```

---

# Why Plugins are Important

Without plugins:

```text
❌ Maven cannot compile code
❌ Maven cannot run tests
❌ Maven cannot package applications
❌ Maven cannot deploy artifacts
```

Plugins provide:
- actual functionality

---

# ⚙️ Plugin Architecture

---

# Basic Workflow

```text
Maven Lifecycle
      ↓
Plugin
      ↓
Goal
      ↓
Task Execution
```

---

# Example

```text
compile phase
      ↓
maven-compiler-plugin
      ↓
compile goal
      ↓
Java source compiled
```

---

# 🌟 What is a Plugin Goal?

> Goal = specific task executed by plugin.

---

# Example

| Plugin | Goal |
|---|---|
| Compiler Plugin | compile |
| Surefire Plugin | test |
| Clean Plugin | clean |
| Jar Plugin | jar |

---

# Example Command

```bash
mvn compiler:compile
```

---

# 🔄 Plugin Execution

Plugins are attached to:
- lifecycle phases

---

# Example

```text
compile phase
      ↓
compiler plugin runs automatically
```

---

# Important Concept

When phase executes:
- related plugin goals execute automatically

---

# 📦 Types of Maven Plugins

---

# 1. Build Plugins

Used during:
- build lifecycle

---

# Examples

```text
✔ Compiler Plugin
✔ Surefire Plugin
✔ Shade Plugin
✔ Jar Plugin
```

---

# 2. Reporting Plugins

Used for:
- reports
- documentation

---

# Examples

```text
✔ Javadoc Plugin
✔ Checkstyle Plugin
✔ PMD Plugin
```

---

# 🏗️ Plugin Configuration in POM.xml

Plugins configured inside:

```xml
<build>
    <plugins>
    </plugins>
</build>
```

---

# Example Structure

```xml
<build>

    <plugins>

        <plugin>

            <groupId>org.apache.maven.plugins</groupId>

            <artifactId>maven-compiler-plugin</artifactId>

            <version>3.11.0</version>

        </plugin>

    </plugins>

</build>
```

---

# 🌟 Maven Compiler Plugin

Used to:
- compile Java source code

---

# Most Important Plugin

Without this:
- Java code cannot compile

---

# Example Configuration

```xml
<plugin>

    <groupId>org.apache.maven.plugins</groupId>

    <artifactId>maven-compiler-plugin</artifactId>

    <version>3.