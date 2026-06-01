
# Microservices Architecture

![Architecture](https://img.shields.io/badge/Architecture-Microservices-blue)
![Docker](https://img.shields.io/badge/Container-Docker-green)
![Cloud](https://img.shields.io/badge/Cloud-Native-orange)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-red)
![Scalability](https://img.shields.io/badge/Scalability-High-success)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Definition](#-definition)
- [Core Principles](#-core-principles)
- [Architecture Diagram](#-architecture-diagram)
- [Microservices Workflow](#-microservices-workflow)
- [Database Per Service Pattern](#-database-per-service-pattern)
- [Real-World Examples](#-real-world-examples)
- [Advantages of Microservices](#-advantages-of-microservices)
- [Disadvantages of Microservices](#-disadvantages-of-microservices)
- [Monolithic vs Microservices](#-monolithic-vs-microservices)
- [When to Use Microservices](#-when-to-use-microservices)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Microservices Architecture is a modern software development approach where an application is divided into multiple small independent services.

Each service:
- Performs one business function
- Has its own database
- Can be deployed independently
- Communicates using APIs

Microservices solve many limitations of:
- Monolithic applications
- Large tightly coupled systems

---

# 🧠 Definition

> Microservices Architecture is an architectural style in which a large application is divided into small, loosely coupled, independently deployable services that communicate using APIs.

---

# 🏗️ Core Idea

Instead of one large application:

```text
One Big Application
```

we divide it into:

```text
User Service
Product Service
Payment Service
Order Service
Notification Service
```

Each service works independently.

---

# ⚙️ Core Principles

---

# 1️⃣ Decomposition

Large applications are divided into:
- Smaller services
- Independent modules

---

## Example

### E-Commerce Platform

```text
Monolithic Application
        ↓
Split Into Services
        ↓
✔ User Service
✔ Product Service
✔ Cart Service
✔ Order Service
✔ Payment Service
✔ Notification Service
```

---

# 2️⃣ Business-Oriented Services

Services are divided according to business functionality.

---

## Correct Way

```text
✔ Payment Service
✔ User Service
✔ Order Service
```

---

## Wrong Way

```text
✘ Database Service
✘ API Service
✘ UI Service
```

Microservices should represent:
- Business capabilities
- Real-world functionalities

---

# 3️⃣ Loose Coupling

Services communicate through APIs.

---

## Benefits

```text
✔ Independent updates
✔ Independent deployment
✔ Easier maintenance
✔ Technology flexibility
```

---

# 4️⃣ Independent Deployment

Each service can be deployed separately.

---

## Example

```text
Update Payment Service
        ↓
Deploy only Payment Service
        ↓
Other services continue running
```

---

# 5️⃣ Database Per Service

Each service owns its own database.

---

# Example

| Service | Database |
|---|---|
| User Service | MySQL |
| Product Service | MongoDB |
| Payment Service | PostgreSQL |

---

# 🏛️ Architecture Diagram

```text
                     ┌───────────────────┐
                     │   API Gateway     │
                     └─────────┬─────────┘
                               │
        ┌──────────┬───────────┼──────────┬──────────┐
        │          │           │          │          │
        ▼          ▼           ▼          ▼          ▼

 ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐
 │ User     │ │ Product  │ │ Order    │ │ Payment  │ │ Notification│
 │ Service  │ │ Service  │ │ Service  │ │ Service  │ │ Service     │
 └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬───────┘
      │             │             │             │             │
      ▼             ▼             ▼             ▼             ▼

 ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌──────────┐
 │ MySQL   │ │MongoDB  │ │MongoDB  │ │Postgres │ │ Redis    │
 └─────────┘ └─────────┘ └─────────┘ └─────────┘ └──────────┘
```

---

# 🌐 API Gateway

API Gateway acts as:
- Entry point for clients
- Request router
- Security layer

---

## Responsibilities

| Function | Purpose |
|---|---|
| Routing | Send requests to correct service |
| Authentication | Validate users |
| Rate Limiting | Prevent overload |
| Monitoring | Track API usage |

---

# 🔄 Microservices Workflow

# Example: Place Order

```text
User clicks "Buy Now"
        ↓
API Gateway receives request
        ↓
Order Service creates order
        ↓
Product Service checks stock
        ↓
Payment Service processes payment
        ↓
Notification Service sends email
        ↓
Order confirmation shown
```

---

# 🔌 API Communication Example

---

## User Service API

```http
GET /users/101
```

### Response

```json
{
  "id": 101,
  "name": "Komal",
  "email": "komal@example.com"
}
```

---

## Product Service API

```http
GET /products/500
```

### Response

```json
{
  "id": 500,
  "name": "Laptop",
  "price": 55000
}
```

---

# 🗄️ Database Per Service Pattern

---

# Monolithic Database

```text
All Services
      ↓
 Single Database
```

---

# Problems

```text
✘ Tight coupling
✘ Difficult scaling
✘ Risky schema changes
✘ Shared dependencies
```

---

# Microservices Database Model

```text
User Service      → MySQL
Product Service   → MongoDB
Payment Service   → PostgreSQL
Notification      → Redis
```

---

# Benefits

```text
✔ Independent scaling
✔ Better security
✔ Service isolation
✔ Technology flexibility
✔ Easier maintenance
```

---

# 📊 Database Comparison

| Service | Database | Reason |
|---|---|---|
| User Service | MySQL | Structured user data |
| Product Service | MongoDB | Flexible product schema |
| Payment Service | PostgreSQL | Strong transaction support |
| Notification Service | Redis | Fast queue handling |

---

# 🌍 Real-World Examples

---

# 🛒 Amazon

Amazon uses hundreds of microservices.

---

## Services Used

| Service | Purpose |
|---|---|
| User Service | Authentication |
| Product Service | Product catalog |
| Cart Service | Shopping cart |
| Payment Service | Transactions |
| Recommendation Service | Product suggestions |
| Shipping Service | Delivery tracking |

---

## Benefits to Amazon

```text
✔ Massive scalability
✔ Faster deployment
✔ Independent teams
✔ Better reliability
```

---

# 🎬 Netflix

Netflix uses microservices for:
- Streaming
- Recommendations
- Billing
- User management

---

## Example Services

| Service | Function |
|---|---|
| Streaming Service | Video delivery |
| Recommendation Engine | Suggest movies |
| Billing Service | Subscription payments |
| Search Service | Search functionality |

---

# 🚀 Advantages of Microservices

---

# 1️⃣ Independent Scalability

Scale only required services.

---

## Example

```text
High traffic on Payment Service
        ↓
Scale only Payment Service
```

---

# Benefit

```text
✔ Lower cost
✔ Better performance
✔ Efficient resource usage
```

---

# 2️⃣ Independent Deployment

Deploy services separately.

---

## Example

```text
Fix bug in Notification Service
        ↓
Deploy only Notification Service
```

---

# 3️⃣ Technology Flexibility

Different services can use different technologies.

---

# Example

| Service | Technology |
|---|---|
| User Service | Java |
| AI Service | Python |
| Search Service | Elasticsearch |
| API Gateway | Node.js |

---

# 4️⃣ Fault Isolation

Failure in one service does not crash entire application.

---

## Example

```text
Recommendation Service fails
        ↓
Users can still place orders
```

---

# 5️⃣ Parallel Development

Multiple teams work independently.

---

## Example

```text
Team A → Payment Service
Team B → Product Service
Team C → Notification Service
```

---

# 6️⃣ Faster Development

Smaller services are easier to:
- Build
- Test
- Deploy
- Maintain

---

# 7️⃣ Easier Maintenance

Small codebases are easier to understand.

---

# 📈 Advantages Summary

| Advantage | Benefit |
|---|---|
| Independent Scaling | Resource optimization |
| Independent Deployment | Faster releases |
| Fault Isolation | Better reliability |
| Technology Flexibility | Best tool selection |
| Parallel Development | Faster development |
| Small Services | Easier maintenance |

---

# ❌ Disadvantages of Microservices

---

# 1️⃣ Complex Architecture

Managing many services becomes difficult.

---

# 2️⃣ Network Communication Overhead

Services communicate over network APIs.

---

## Result

```text
API calls slower than internal method calls
```

---

# 3️⃣ Difficult Debugging

Need distributed tracing tools.

---

# 4️⃣ Higher Infrastructure Cost

Requires:
- Containers
- Kubernetes
- Monitoring tools
- CI/CD pipelines

---

# 5️⃣ Data Consistency Challenges

Multiple databases create synchronization challenges.

---

# 6️⃣ Monitoring Complexity

Need advanced monitoring systems.

---

# 📊 Advantages vs Disadvantages

| Advantages | Disadvantages |
|---|---|
| Highly scalable | Complex architecture |
| Independent deployment | Network overhead |
| Better reliability | Hard debugging |
| Flexible technology | More infrastructure |
| Faster releases | Monitoring complexity |

---

# ⚔️ Monolithic vs Microservices

| Feature | Monolithic | Microservices |
|---|---|---|
| Deployment | Single Unit | Independent Services |
| Database | Shared | Separate |
| Scaling | Entire App | Individual Services |
| Failure Impact | Entire App | Isolated |
| Technology Stack | Single | Multiple |
| Development Teams | Large Team | Small Teams |
| Flexibility | Low | High |

---

# 📌 When to Use Microservices

---

# Suitable For

```text
✔ Large applications
✔ Cloud-native systems
✔ High scalability needs
✔ Large development teams
✔ Frequent deployments
✔ Enterprise systems
```

---

# Not Suitable For

```text
✘ Small projects
✘ Simple applications
✘ Small teams
✘ Limited infrastructure budget
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Microservices | Small independent services |
| Communication | APIs |
| Database | Separate per service |
| Scalability | Independent |
| Deployment | Independent |
| Coupling | Loose coupling |
| Architecture | Distributed |

---

# 🧠 Important Keywords

- Microservices
- API Gateway
- Loose Coupling
- Scalability
- Distributed System
- Independent Deployment
- Containerization
- Service Discovery
- Fault Isolation
- Polyglot Architecture

---

# ❓ Viva Questions

1. What are microservices?
2. What is loose coupling?
3. Why are APIs used in microservices?
4. What is API Gateway?
5. Why does each service have its own database?
6. What are advantages of microservices?
7. Difference between monolithic and microservices?
8. What is fault isolation?
9. Why is scaling easier in microservices?
10. What is distributed architecture?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why are microservices popular? | Scalability and flexibility |
| Main advantage of microservices? | Independent deployment |
| Biggest challenge in microservices? | Complexity |
| Why use API Gateway? | Centralized routing and security |
| Why separate databases? | Better service independence |

---

# 📌 Key Takeaway

Microservices architecture transforms:

```text
One Large Application
            ↓
Multiple Independent Services
```

This provides:
- Better scalability
- Faster deployment
- Fault isolation
- Technology flexibility

BUT

It also introduces:
- Complexity
- Network overhead
- Monitoring challenges

---

# ✅ Conclusion

Microservices architecture is the foundation of modern cloud-native applications.

Companies like:
- Amazon
- Netflix
- Uber
- Spotify

use microservices to achieve:
- Massive scalability
- Faster development
- Independent deployments
- High availability

Microservices work best when combined with:
- Docker
- Kubernetes
- CI/CD
- Cloud Computing

---

# 🔗 Next Topic

➡️ Containers and Docker