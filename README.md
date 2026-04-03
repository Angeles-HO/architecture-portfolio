# 🏗️ Architecture Portfolio

> **Note**: This repository showcases the architecture, design patterns, and technical decisions from my private projects. No business logic or sensitive code is included.

## 📋 Overview

Most of my professional work is developed in **private repositories** for clients and production environments. This portfolio demonstrates:

- **System Architecture** & Design Decisions
- **Technical Patterns** & Best Practices
- **Security Implementations**
- **DevOps & Infrastructure** Setup
- **Problem-Solving Approaches**

---

## 🎯 Featured Projects

### 1. [E-commerce Cosmetics Platform](./projects/ecommerce-cosmetics/)

Full-stack e-commerce application with advanced security features.

**Tech Stack**: Node.js · Express · PostgreSQL · Redis · Docker · Nginx  
**Highlights**: Custom CSRF protection · Session management · Cart system · Rate limiting

### 2. [Digital Menu System (QR)](./projects/digital-menu-qr/)

QR-based digital menu with real-time updates and caching.

**Tech Stack**: Node.js · PostgreSQL · Docker · Redis  
**Highlights**: Cache strategy · Data synchronization · Background jobs

### 3. [Telvyn - Local-First Agent Runtime](./projects/telvyn/)

Local-first technical agent runtime with deterministic workspace I/O and session continuity.

**Tech Stack**: Python · CLI/TUI · Local LLM backends  
**Highlights**: Deterministic workspace contract · Session/Run memory model · Guardrailed execution

### 4. [Kitsunping Network Optimization Stack](./projects/kitsunping-network-stack/)

Android network optimization stack combining on-device profile orchestration and router-side policy protocol.

**Tech Stack**: Bash · Android root ecosystem · Router scripting  
**Highlights**: Event-driven daemon · QoS policy protocol · RF channel recommendation · Router/client integration boundary

---

## 🔧 Technical Patterns

Detailed documentation of reusable patterns and implementations:

- [**CSRF Protection**](./patterns/csrf-implementation.md) - Token-based implementation with session binding
- [**Redis Session Strategy**](./patterns/redis-session-strategy.md) - Session management with Redis backend
- [**Rate Limiting**](./patterns/rate-limiting.md) - Multi-tier request throttling
- [**Docker Multi-Service Setup**](./patterns/docker-compose-setup.md) - Container orchestration patterns
- [**Database Migrations**](./patterns/database-migrations.md) - Version control for database schemas

---

## 🛠️ Tech Stack Summary

### Backend

- **Languages**: JavaScript/Node.js, TypeScript, Python, Java, Bash
- **Frameworks**: Express.js, Sequelize ORM
- **Databases**: PostgreSQL, Redis, MySQL, MongoDB

### DevOps & Infrastructure

- **Containerization**: Docker, Docker Compose
- **Web Servers**: Nginx, Reverse Proxy configurations
- **CI/CD**: Automated migrations, health checks

### Security

- Custom CSRF protection implementation
- Session security with Redis
- Password hashing (bcrypt, argon2)
- Request rate limiting
- Input sanitization & validation
- Deterministic workspace I/O guardrails

---

## 📊 Architecture Principles

All projects follow these core principles:

- **Separation of Concerns** - Clear MVC/layered architecture
- **Security First** - Defense in depth approach
- **Scalability** - Horizontal scaling ready
- **Maintainability** - Clean code, documented patterns
- **Performance** - Caching strategies, optimized queries

---

## 📖 How to Navigate

Each project folder contains a project README with:

- Architecture overview and system boundaries
- Tech stack and rationale
- Core modules and data/control flow
- Technical trade-offs and implementation notes

Pattern documentation includes:

- Problem statement
- Solution approach
- Code examples (simplified)
- Trade-offs and considerations

---

## 🌟 Highlights

- **Clean Architecture**: Consistent layered structure across all projects
- **Production-Ready**: Deployed applications serving real users
- **Security-Focused**: Custom implementations beyond standard libraries
- **DevOps Skills**: Complete Docker setups with multi-service orchestration
- **Runtime Design**: Deterministic contracts and continuity models for agent workflows
- **Networking Systems**: Router-side protocol design, QoS/PPC flows, and RF channel recommendation strategies
- **Problem Solver**: Documented real-world challenges and solutions

---

## 📫 Contact

Interested in discussing these architectures or potential collaboration?

- **GitHub**: [@Angeles-HO](https://github.com/Angeles-HO)
- **Email**: [Angeles-HO](mailto:angelesho@pm.me)
- **Profile**: [View Full Tech Stack](https://github.com/Angeles-HO/Angeles-HO)

---

<p align="center">
  <i>Building secure, scalable, and maintainable systems</i>
</p>
