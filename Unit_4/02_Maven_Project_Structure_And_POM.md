# Maven Project Structure & POM.xml

![Maven](https://img.shields.io/badge/Maven-POM.xml-blue)
![Java](https://img.shields.io/badge/Java-ProjectStructure-green)
![DevOps](https://img.shields.io/badge/DevOps-BuildAutomation-orange)
![XML](https://img.shields.io/badge/XML-Configuration-red)

---

# 📚 Table of Contents

- Introduction
- Standard Maven Directory Structure
- Why Standard Structure Matters
- Understanding POM.xml
- POM Structure
- Maven Coordinates
- Project Metadata
- Dependencies
- Repositories
- Build Section
- Plugins
- Parent POM
- Effective POM
- Real-World Example
- Best Practices
- Summary

---

# 📖 Introduction

Maven follows:
- convention over configuration

This means:
- every Maven project follows a standard structure

Maven automatically understands:
- source code location
- test location
- resources
- output folders

without extra configuration.

---

# 🎯 Why Standard Structure Matters

Without standardization:

```text
❌ Every project looks different
❌ Difficult collaboration
❌ Build confusion
❌ Hard CI/CD integration
❌ Difficult maintenance
```

---

# Maven Standardization Solves

```text
✔ Easy collaboration
✔ Faster onboarding
✔ Predictable builds
✔ Better automation
✔ Industry standard structure
```

---

# 📂 Standard Maven Directory Structure

---

# Complete Structure

```text
my-project/
│
├── pom.xml
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   ├── resources/
│   │   └── webapp/
│   │
│   └── test/
│       ├── java/
│       └── resources/
│
├── target/
│
└── README.md
```

---

# 🧠 Important Directories

| Directory | Purpose |
|---|---|
| `src/main/java` | Main application code |
| `src/main/resources` | Config files/resources |
| `src/test/java` | Unit tests |
| `src/test/resources` | Test resources |
| `target` | Build output |
| `pom.xml` | Maven configuration |

---

# 📁 src/main/java

Contains:
- application source code

---

# Example

```text
src/main/java/com/example/App.java
```

---

# 📁 src/main/resources

Contains:
- configuration files
- properties files
- static resources

---

# Example

```text
application.properties
log4j.xml
config.yml
```

---

# 📁 src/test/java

Contains:
- unit test classes

---

# Example

```text
AppTest.java
```

---

# 📁 target Folder

Generated automatically during build.

Contains:
- compiled classes
- JAR/WAR files
- reports

---

# Example

```text
target/myapp.jar
```

---

# 📄 What is POM.xml?

> POM = Project Object Model

Main configuration file of Maven project.

---

# Purpose of POM.xml

```text
✔ Project information
✔ Dependency management
✔ Plugin configuration
✔ Build settings
✔ Repository configuration
✔ Packaging instructions
```

---

# File Name

```text
pom.xml
```

---

# 📦 Basic POM Structure

```xml
<project>
    
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>

    <artifactId>myapp</artifactId>

    <version>1.0.0</version>

</project>
```

---

# 🧠 Maven Coordinates

Every Maven project is uniquely identified using:

```text
groupId
artifactId
version
```

---

# Coordinate Example

```xml
<groupId>com.company</groupId>

<artifactId>student-management</artifactId>

<version>1.0.0</version>
```

---

# Meaning

| Element | Purpose |
|---|---|
| `groupId` | Organization/project group |
| `artifactId` | Project name |
| `version` | Project version |

---

# Example Output Artifact

```text
student-management-1.0.0.jar
```

---

# 🌟 Complete POM Example

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>

    <artifactId>demo-app</artifactId>

    <version>1.0.0</version>

    <packaging>jar</packaging>

    <name>Demo Maven App</name>

    <description>Simple Maven Project</description>

</project>
```

---

# 📦 Packaging Types

| Packaging | Purpose |
|---|---|
| `jar` | Java applications |
| `war` | Web applications |
| `pom` | Parent projects |
| `ear` | Enterprise applications |

---

# Example

```xml
<packaging>jar</packaging>
```

---

# 📚 Dependencies in POM

Dependencies are external libraries required by project.

---

# Example Dependency

```xml
<dependencies>

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
    </dependency>

</dependencies>
```

---

# Result

Maven automatically downloads:
- JUnit library
- transitive dependencies

---

# 🌍 Maven Repositories

Dependencies downloaded from:
- repositories

---

# Central Repository

Default Maven repository.

---

# Example Repository

```xml
<repositories>

    <repository>
        <id>central</id>
        <url>https://repo.maven.apache.org/maven2</url>
    </repository>

</repositories>
```

---

# ⚙️ Build Section

Defines:
- build behavior
- plugins
- packaging rules

---

# Example

```xml
<build>

    <plugins>

    </plugins>

</build>
```

---

# 🔌 Maven Plugins

Plugins add functionality to Maven.

---

# Common Plugins

| Plugin | Purpose |
|---|---|
| Compiler Plugin | Compile Java |
| Surefire Plugin | Run tests |
| Shade Plugin | Create Uber JAR |
| Jar Plugin | Generate JAR |

---

# Example Compiler Plugin

```xml
<build>

    <plugins>

        <plugin>

            <groupId>org.apache.maven.plugins</groupId>

            <artifactId>maven-compiler-plugin</artifactId>

            <version>3.11.0</version>

            <configuration>

                <source>17</source>

                <target>17</target>

            </configuration>

        </plugin>

    </plugins>

</build>
```

---

# 👨‍👩‍👧 Parent POM

Parent POM allows:
- sharing common configuration

across multiple projects.

---

# Example

```xml
<parent>

    <groupId>org.springframework.boot</groupId>

    <artifactId>spring-boot-starter-parent</artifactId>

    <version>3.2.0</version>

</parent>
```

---

# Benefits

```text
✔ Shared dependency versions
✔ Common plugin configuration
✔ Centralized management
✔ Cleaner child POMs
```

---

# 🌟 Effective POM

Effective POM =
- final combined configuration

after inheritance and defaults applied.

---

# Command

```bash
mvn help:effective-pom
```

---

# 🛠️ Create Maven Project

---

# Command

```bash
mvn archetype:generate
```

---

# Maven Asks For

```text
groupId
artifactId
version
package
```

---

# Generated Structure

```text
✔ Standard folders
✔ pom.xml
✔ Sample source code
✔ Sample test
```

---

# 🌍 Real-World Example

---

# Spring Boot POM

```xml
<project>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.0</version>
    </parent>

    <groupId>com.example</groupId>

    <artifactId>spring-demo</artifactId>

    <version>1.0.0</version>

    <dependencies>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

    </dependencies>

</project>
```

---

# Result

```text
✔ Web server support
✔ Spring dependencies
✔ Embedded Tomcat
✔ REST APIs
```

---

# 🔐 Best Practices

---

# Use Meaningful groupId

✅ Good

```xml
com.company.project
```

---

# Use Semantic Versioning

```text
1.0.0
1.1.0
2.0.0
```

---

# Keep Dependencies Minimal

Avoid unnecessary libraries.

---

# Use Parent POMs

For enterprise projects.

---

# Use Plugin Versions

Always specify:
- plugin versions

---

# 📊 Maven Project Workflow

```text
Source Code
     ↓
pom.xml
     ↓
Dependencies Downloaded
     ↓
Compile
     ↓
Test
     ↓
Package
     ↓
Artifact (JAR/WAR)
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| POM.xml | Maven configuration file |
| groupId | Organization identifier |
| artifactId | Project name |
| version | Application version |
| dependency | External library |
| plugin | Maven extension |
| target | Build output folder |

---

# 🧠 Important Keywords

- POM.xml
- Maven Coordinates
- Dependencies
- Plugins
- Parent POM
- Build Section
- Maven Repository
- Packaging
- Artifact
- Effective POM

---

# ❓ Viva Questions

1. What is POM.xml?
2. What is Maven project structure?
3. What is groupId?
4. What is artifactId?
5. What is dependency?
6. What is plugin in Maven?
7. What is Parent POM?
8. What is target folder?
9. What is packaging type?
10. What is Effective POM?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is POM.xml? | Maven project configuration |
| What is groupId? | Organization identifier |
| What is artifactId? | Project name |
| What is Maven dependency? | External library |
| Why use Parent POM? | Shared configuration |

---

# ✅ Conclusion

Maven standardizes:
- Java project structure
- dependency management
- plugin configuration
- build automation

Using:
- POM.xml
- dependencies
- plugins
- repositories

developers can build:
- scalable applications
- enterprise systems
- CI/CD pipelines
- cloud-native Java applications

Understanding Maven project structure is essential for:
- Spring Boot
- Microservices
- DevOps
- Backend Development