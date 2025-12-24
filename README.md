# Cortex Platform

[<img src="https://img.shields.io/badge/build-passing-brightgreen">]()
<a href="https://www.java.com"><img src="https://img.shields.io/badge/Java-21-orange"></a>
<a href="https://spring.io/projects/spring-boot"><img src="https://img.shields.io/badge/Spring_Boot-3.4-green"></a>
<a href="https://fastapi.tiangolo.com/"><img src="https://img.shields.io/badge/FastAPI-0.109-blue"></a>
[<img src="https://img.shields.io/badge/license-MIT-blue">]()

> **A High-Performance Modular Monolith demonstrating Polyglot Orchestration.**
> *Spring Boot 3.4 (Core) + FastAPI (AI/Data) + Vue 3 (Client)*

---

## 🏗 Architectural Strategy

Cortex Platform is engineered as a **Modular Monolith**. It leverages the robustness of the Java ecosystem for core business logic and security, while seamlessly offloading high-compute AI tasks to a specialized Python worker. 

This architecture minimizes infrastructure overhead while maintaining strict service boundaries using Docker orchestration.

```mermaid
graph LR
    User((User)) -->|HTTPS| Nginx[Nginx Gateway]
    Nginx -->|/api| Spring[Spring Boot 3.4 Core]
    
    subgraph Internal Docker Network
    Spring -->|Sync HTTP Client| Python[FastAPI AI Worker]
    Python -->|Read/Write| DB[(Neon Serverless DB)]
    end
    
    style Spring fill:#6db33f,stroke:#333,stroke-width:2px,color:white
    style Python fill:#3776ab,stroke:#333,stroke-width:2px,color:white
    style Nginx fill:#009639,stroke:#333,stroke-width:2px,color:white
    style DB fill:#00e599,stroke:#333,stroke-width:2px
```