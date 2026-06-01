# Jenkins Security, Users and Roles

![Jenkins](https://img.shields.io/badge/Jenkins-Security-red)
![DevOps](https://img.shields.io/badge/DevOps-Best_Practices-blue)
![RBAC](https://img.shields.io/badge/RBAC-Authorization-green)
![CI/CD](https://img.shields.io/badge/CI/CD-Secure-orange)

---

# 📚 Table of Contents

- Why Security Matters in Jenkins
- Authentication
- Authorization
- Users in Jenkins
- Roles in Jenkins
- Role-Based Access Control (RBAC)
- Credentials Management
- Secrets Management
- SSH Keys in Jenkins
- API Tokens
- Secure Pipeline Practices
- Jenkins Security Best Practices
- Common Security Risks
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# Why Security Matters in Jenkins?

Jenkins controls:

- Source Code
- Build Pipelines
- Docker Images
- Cloud Infrastructure
- Production Deployments
- Secrets & Credentials

If Jenkins is compromised:

```text
Source Code Theft
Deployment Abuse
Credential Leakage
Production Outages
```

may occur.

---

# Jenkins Security Layers

```text
User Authentication
        ↓
Authorization
        ↓
Credentials Protection
        ↓
Pipeline Security
        ↓
Infrastructure Security
```

---

# Authentication

Authentication answers:

```text
Who are you?
```

Jenkins verifies the identity of users before allowing access.

---

# Authentication Methods

### 1. Jenkins Internal Database

Users stored inside Jenkins.

Example:

```text
admin
developer
tester
```

---

### 2. LDAP Authentication

Enterprise environments often use:

```text
Microsoft Active Directory
LDAP
```

for centralized login.

---

### 3. GitHub Authentication

Users login using GitHub accounts.

---

### 4. Google Authentication

OAuth-based login.

---

### 5. SAML / Single Sign-On

Used in large organizations.

Examples:

- Okta
- Azure AD
- OneLogin

---

# Authentication Flow

```text
User
  ↓
Login Screen
  ↓
Credential Verification
  ↓
Access Granted
```

---

# Authorization

Authorization answers:

```text
What can you do?
```

Even after login, not every user gets full access.

---

# Example

Admin:

```text
Create Jobs
Delete Jobs
Manage Plugins
Manage Users
```

Developer:

```text
Build Jobs
View Logs
```

Tester:

```text
View Results
Run Tests
```

---

# Authorization Flow

```text
Login
  ↓
User Identified
  ↓
Role Checked
  ↓
Permissions Granted
```

---

# Users in Jenkins

Users represent people accessing Jenkins.

Examples:

```text
admin
komal
developer1
tester1
```

---

# Creating Users

Navigate:

```text
Manage Jenkins
    ↓
Security
    ↓
Users
```

---

# User Information

Each user has:

- Username
- Password
- Email
- API Token
- Permissions

---

# Jenkins User Types

## Administrator

Full control.

Can:

✔ Install Plugins

✔ Create Users

✔ Configure Jenkins

✔ Manage Pipelines

---

## Developer

Can:

✔ Trigger Builds

✔ View Logs

✔ Access Pipelines

---

## Tester

Can:

✔ Execute Test Jobs

✔ View Reports

---

## Viewer

Can:

✔ View Dashboard

✔ View Build Results

Cannot modify anything.

---

# Roles in Jenkins

Roles define permissions.

Instead of assigning permissions individually:

```text
User
    ↓
Role
    ↓
Permissions
```

---

# Example Roles

```text
Admin
Developer
Tester
Viewer
```

---

# Role-Based Access Control (RBAC)

RBAC simplifies security management.

---

# RBAC Architecture

```text
User
  ↓
Role
  ↓
Permissions
```

Example:

```text
Komal
   ↓
Developer Role
   ↓
Build + Read Access
```

---

# Why RBAC?

Without RBAC:

```text
100 Users
100 Permission Configurations
```

Hard to manage.

With RBAC:

```text
100 Users
4 Roles
```

Easy management.

---

# Typical RBAC Model

| Role | Permissions |
|--------|-------------|
| Admin | Full Control |
| Developer | Build & Configure |
| Tester | Run Tests |
| Viewer | Read Only |

---

# Credentials Management

Credentials are sensitive information stored securely in Jenkins.

Examples:

```text
GitHub Token
Docker Hub Password
AWS Keys
SSH Keys
Database Passwords
```

---

# Why Credentials?

Without credentials:

```text
Cannot Access GitHub
Cannot Push Docker Images
Cannot Deploy
```

---

# Jenkins Credentials Store

Navigate:

```text
Manage Jenkins
    ↓
Credentials
```

---

# Credential Types

### Username + Password

Example:

```text
GitHub Login
Docker Hub Login
```

---

### Secret Text

Example:

```text
GitHub PAT
AWS Token
```

---

### SSH Username with Private Key

Used for:

```text
Server Deployment
Git Access
```

---

### Secret File

Examples:

```text
AWS Credentials File
Kubeconfig
```

---

# Credentials Architecture

```text
Pipeline
    ↓
Credential Store
    ↓
Secret Retrieved
    ↓
Deployment
```

---

# Example Credential Usage

```groovy
withCredentials([
string(credentialsId: 'docker-token',
variable: 'TOKEN')
]) {

sh 'echo $TOKEN'

}
```

---

# Secrets Management

Secrets include:

```text
Passwords
Tokens
Private Keys
Certificates
```

Never hardcode secrets inside:

```groovy
Jenkinsfile
```

---

# Wrong Practice

```groovy
password = "admin123"
```

Problem:

```text
Visible in Git Repository
```

---

# Correct Practice

Store in:

```text
Jenkins Credentials Store
```

and access securely.

---

# SSH Keys in Jenkins

SSH keys enable secure communication.

Used for:

- GitHub
- Linux Servers
- Cloud VMs

---

# SSH Authentication Flow

```text
Jenkins
   ↓
Private Key
   ↓
Remote Server
   ↓
Authorized Access
```

---

# Generating SSH Key

Linux:

```bash
ssh-keygen -t rsa -b 4096
```

---

# Files Created

```text
id_rsa
id_rsa.pub
```

---

# Jenkins Stores

```text
id_rsa
```

(private key)

---

# Server Stores

```text
id_rsa.pub
```

(public key)

---

# API Tokens

API Tokens replace passwords.

Used for:

- Jenkins API
- GitHub API
- Docker Registries

---

# Why API Tokens?

Advantages:

✔ More Secure

✔ Revocable

✔ Limited Scope

✔ CI/CD Friendly

---

# Example GitHub PAT

```text
ghp_xxxxxxxxxxxxxx
```

Stored in Jenkins Credentials.

---

# Secure Pipeline Practices

Always:

✔ Use credentials()

✔ Use secret text

✔ Hide passwords

✔ Restrict access

---

# Example

```groovy
environment {

DOCKER_USER = credentials('docker-user')

}
```

---

# Pipeline Security Checklist

✔ No hardcoded secrets

✔ Restricted credentials

✔ Secure agents

✔ Use RBAC

✔ Audit user activity

---

# Common Jenkins Security Risks

## Risk 1: Anonymous Access

Anyone can:

```text
View Jobs
Trigger Builds
```

Dangerous.

---

## Risk 2: Hardcoded Passwords

Example:

```groovy
password="admin"
```

Never do this.

---

## Risk 3: Excessive Permissions

Developer gets:

```text
Admin Access
```

Security violation.

---

## Risk 4: Outdated Plugins

Can contain vulnerabilities.

Always update plugins.

---

## Risk 5: Untrusted Pipelines

Executing unknown code may:

```text
Delete Files
Steal Secrets
```

---

# Jenkins Security Best Practices

## 1. Enable Authentication

Never leave Jenkins public.

---

## 2. Use RBAC

Assign least privilege.

---

## 3. Use HTTPS

Encrypt communication.

---

## 4. Store Secrets Securely

Use Jenkins Credentials.

---

## 5. Update Plugins

Regularly patch vulnerabilities.

---

## 6. Backup Jenkins

Protect against failures.

---

## 7. Audit Access

Monitor user activities.

---

## 8. Restrict Agent Permissions

Agents should not have excessive access.

---

# Enterprise Security Architecture

```text
Developer
     ↓
Authentication
     ↓
Authorization
     ↓
Credentials Store
     ↓
Pipeline
     ↓
Deployment
```

---

# Quick Revision Notes

## Authentication

```text
Who are you?
```

---

## Authorization

```text
What can you do?
```

---

## RBAC

```text
Role-Based Access Control
```

---

## Credentials

```text
Stored Secrets
```

---

## SSH Key

```text
Secure Authentication
```

---

## API Token

```text
Password Alternative
```

---

# Viva Questions

### 1. What is Authentication?

Identity verification.

---

### 2. What is Authorization?

Permission verification.

---

### 3. What is RBAC?

Role-Based Access Control.

---

### 4. Where are secrets stored in Jenkins?

Credentials Store.

---

### 5. Why use API Tokens?

More secure than passwords.

---

### 6. What is an SSH Key?

Secure authentication mechanism.

---

### 7. Can Jenkins integrate with LDAP?

Yes.

---

### 8. Why avoid hardcoded passwords?

Security risk.

---

### 9. What is least privilege?

Grant only necessary permissions.

---

### 10. What is Jenkins Credentials Store?

Secure storage for secrets.

---

# Interview Questions

## Q1. Explain Authentication vs Authorization.

Authentication verifies identity; Authorization verifies permissions.

---

## Q2. What is RBAC in Jenkins?

A role-based permission management system.

---

## Q3. How should secrets be managed in Jenkins?

Using Jenkins Credentials Store.

---

## Q4. Why are API tokens preferred over passwords?

They are more secure, revocable, and suitable for automation.

---

## Q5. What are the major Jenkins security best practices?

Authentication, RBAC, HTTPS, secret management, plugin updates, and auditing.

---

# Key Takeaways

✔ Jenkins security is critical in CI/CD environments.

✔ Authentication verifies identity.

✔ Authorization controls permissions.

✔ RBAC simplifies access management.

✔ Credentials Store protects secrets.

✔ SSH Keys and API Tokens enable secure automation.

✔ Never hardcode passwords in Jenkinsfiles.

✔ Security best practices are essential for production Jenkins environments.

---

# Summary

Jenkins Security focuses on protecting pipelines, credentials, users, and infrastructure. Through Authentication, Authorization, RBAC, Credentials Management, SSH Keys, and API Tokens, organizations can securely automate CI/CD workflows while minimizing security risks and maintaining compliance.