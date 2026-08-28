# Hi there, I'm Akash Gupta 👋

**Backend & Distributed Systems Engineer** | **Java & Cloud-Native Specialist**

I specialize in building scalable, fault-tolerant microservice architectures, event-driven systems, and containerized cloud applications. Passionate about domain-driven design, clean code, and automating modern DevOps pipelines.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/akash-gupta2)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:akashgupta9282@gmail.com)

---

### 💻 Core Tech Stack

| Domain | Technologies |
| :--- | :--- |
| **Languages & Frameworks** | Java 17+, Spring Boot 3, Spring Cloud Gateway, Spring Data JPA, Hibernate |
| **Architecture** | Microservices (Database-per-Service), Event-Driven Architecture, REST APIs |
| **Messaging & Storage** | RabbitMQ, PostgreSQL 15, HikariCP |
| **DevOps & Infrastructure** | Kubernetes, Docker, Minikube |

---

### 🌟 Featured Project: [Cake Delight Microservices Platform](https://github.com/akashgupta2233/cake-delight-cloud-native-microservices)

An event-driven, cloud-native e-commerce platform built to demonstrate high availability, fault isolation, and asynchronous processing using Spring Boot, PostgreSQL, RabbitMQ, and Kubernetes.

```text
                               ┌───────────────────┐
                               │  Spring Cloud     │
                               │  API Gateway      │
                               │  (Port 8080)      │
                               └─────────┬─────────┘
                                         │
        ┌──────────────────┬──────────────┼──────────────┬──────────────────┐
        │ /api/cakes        │ /api/orders  │ /api/ratings │ /api/notifications
        ▼                  ▼              ▼              ▼                  ▼
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌─────────────────┐   ┌──────────────┐
│ Catalog Svc  │   │  Order Svc   │   │  Rating Svc  │   │ Notification Svc│   │   Frontend   │
│ (Port 8082)  │   │ (Port 8083)  │   │ (Port 8084)  │   │   (Port 8085)   │   │ (Port 3000)  │
└──────┬───────┘   └──────┬───────┘   └──────┬───────┘   └────────┬────────┘   └──────────────┘
       │                  │                  │                    │
  (catalog_db)        (order_db)        (rating_db)           (notification_db)
       │                  │                  │                    ▲
       └──────────────────┼──────────────────┴────────────────────┤
                          │  OrderCompletedEvent                  │
                          └──────────► [ RabbitMQ ] ──────────────┘
                                     (order.exchange)

```

**Key Architectural Decisions:**

* **Database-per-Service Pattern:** Isolated 4 dedicated PostgreSQL databases (`catalog_db`, `order_db`, `rating_db`, `notification_db`) to guarantee domain autonomy and zero cross-database lock contention.
* **Resilient Asynchronous Messaging:** Built non-blocking order checkout pipelines. `OrderService` dispatches `OrderCompletedEvent` over RabbitMQ Topic Exchanges (`order.exchange`) with transaction fallbacks to prevent cascading failures.
* **Decoupled Event Processing:** Configured durable `notification.queue` bound via `order.completed` routing keys to process notifications asynchronously without blocking main thread pools.
* **Centralized API Routing:** Implemented Spring Cloud Gateway with dynamic path rewriting (`StripPrefix=2`) for secure downstream request routing.
* **Kubernetes Orchestration:** Fully containerized with production-ready K8s manifests featuring PVC volumes, liveness/readiness probes, and namespace isolation.
