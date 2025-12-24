# Cortex Platform

<a><img src="https://img.shields.io/badge/build-passing-brightgreen"></a>
<a href="https://www.java.com"><img src="https://img.shields.io/badge/Java-21-orange"></a>
<a href="https://spring.io/projects/spring-boot"><img src="https://img.shields.io/badge/Spring_Boot-3.4-green"></a>
<a href="https://fastapi.tiangolo.com/"><img src="https://img.shields.io/badge/FastAPI-0.109-blue"></a>
<a><img src="https://img.shields.io/badge/license-MIT-blue"></a>

> **A High-Performance Modular Monolith demonstrating Polyglot Orchestration.**
> *Spring Boot 3.4 (Core) + FastAPI (AI/Data) + Vue 3 (Client)*

---

## 🏗 Architectural Strategy

Cortex Platform is engineered as a **Modular Monolith**. It leverages the robustness of the Java ecosystem for core business logic and security, while seamlessly offloading high-compute AI tasks to a specialized Python worker.

The diagram below illustrates the network topology: Nginx acts as the secure entry point, proxying traffic to the Spring Boot core within the private Docker network. Spring Boot then orchestrates asynchronous data tasks with the Python worker, which persists data to the external Serverless Postgres instance.

```mermaid
graph LR
    User((User)) -->|HTTPS| Nginx[Nginx Gateway]
    
    subgraph "Private Docker Network"
    Nginx -->|Proxy /api| Spring[Spring Boot 3.4 Core]
    Spring -->|Sync HTTP Client| Python[FastAPI AI Worker]
    end

    Python -->|External SSL| DB[(Neon Serverless DB)]
    
    style Spring fill:#6db33f,stroke:#333,stroke-width:2px,color:white
    style Python fill:#3776ab,stroke:#333,stroke-width:2px,color:white
    style Nginx fill:#009639,stroke:#333,stroke-width:2px,color:white
    style DB fill:#00e599,stroke:#333,stroke-width:2px
```