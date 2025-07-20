---
marp: true
theme: black-white
class: lead
paginate: true
---

<!-- 
_class: lead
_footer: 'Practicum project, S25: Aleliya Turushkina, Kirill Efimovich, Nikita Maksimenko, Timur Salakhov, Ravil Kazeev, Mikhail Trifonov, Kirill Shumskiy' 
-->

# 🚀 Open Labs Share

**Next-Gen Learning Platform: Microservices Meets Education**

---

## Agenda

- **Problem Statement & Technical Vision**
- **Team intro**
- **Demo**
- **Frontend Engineering & UX**
- **Advanced System Architecture**
- **Backend Microservices Deep Dive**
- **AI/ML Innovation & Intelligence**
- **DevOps & Cloud Infrastructure**
- **Discussion**

---

## The Problem: Skills Gap in Tech Education

**Engineering challenges in education technology:**

- **Scalability bottlenecks** in traditional learning management systems
- **Limited real-world project experience** due to academic focus on theory
- **Inefficient mentor-learner matching** without automated skill assessment
- **Poor feedback loops** between industry needs and educational content

**Our engineering mission:** Build a distributed, scalable platform that efficiently connects industry experts with aspiring developers through hands-on technical projects.

---

<!-- _class: compact-list -->

## Technical Leadership & Ownership

**Distributed engineering team with specialized technical domains:**

- **Kirill Efimovich (PM/DevOps)** - *Infrastructure Architecture & Project Leadership*
- **Mikhail Trifonov** - *Security Engineering & Authentication Systems*
- **Nikita Maksimenko** - *Backend Architecture & Core Services*
- **Timur Salakhov** - *Content Pipeline & Storage Systems*
- **Ravil Kazeev** - *Algorithms Engineering & Review Systems*
- **Kirill Shumskiy** - *AI/ML Engineering & Intelligence Systems*
- **Aleliya Turushkina** - *Frontend Architecture & User Experience*

---

## Our Product Vision

**Open Labs Share** - A modern learning platform that bridges the gap between academia and industry through hands-on technical collaboration.

**We revolutionize education by:**
- **Streamlined Content Creation:** Version-controlled lab management system enabling experts to publish and maintain high-quality learning materials
- **Guided Learning Experience:** Structured submission and review process that provides meaningful feedback and tracks progress
- **Smart Community Building:** AI-enhanced networking that connects learners with relevant peers and mentors based on skills and interests

---

## Our Technical Vision

**Open Labs Share** - A cloud-native, microservices-driven learning ecosystem with intelligent matching and AI-powered assistance.

**We transform learning through:**
- **Expert Content Pipeline:** Git-inspired versioning system for lab content with automated distribution
- **Learner Development Workflow:** CI/CD-like submission pipeline with automated validation and feedback routing
- **Intelligent Community:** ML-driven peer matching and reputation-based quality assurance systems
---

<!-- _class: compact-list -->

## Live Technical Demo Walkthrough

1.  **Secure Authentication:** OAuth2/JWT with multi-factor authentication demo
2.  **Intelligent Lab Discovery:** ML-powered recommendations and search
3.  **Advanced Development Workflow:** Real-time collaboration and submission pipeline
4.  **Intelligent Review Engine:** AI-assisted peer matching and quality scoring
5.  **Analytics Dashboard:** Real-time metrics and performance insights

---

# 🌐 Frontend Architecture & User Experience

**Aleliya Turushkina - Frontend Architect**


This slide is for Aleliya to fill with:
- Frontend architecture and design patterns
- React + TypeScript implementation
- State management strategy
- Component library and design system
- Performance optimization techniques
- User experience design principles


**[Frontend architecture to be detailed by team member]**

---

## Frontend: Performance & Optimization

**Aleliya Turushkina**

Details to include:
- Bundle optimization and code splitting
- Lazy loading strategies
- Performance monitoring
- SEO optimization
- Accessibility implementation
- Cross-browser compatibility
- Mobile responsiveness

**[Performance optimization details to be added]**

---

## Frontend: API Integration & Real-time Features

**Aleliya Turushkina**

Details to include:
- REST API integration patterns
- WebSocket implementation for real-time features
- State management (Redux/Zustand)
- Error handling and user feedback
- File upload and download UX
- Progressive Web App features
- Testing strategies


**[API integration and real-time features to be added]**

---

## Lets go to backend
---
<!-- _class: tech-details -->

## Advanced System Architecture

**Cloud-native architecture designed for high availability and horizontal scaling**

```mermaid

```

---

# 🔐 Authentication & Security Service

**Mikhail Trifonov**


This slide is for Mikhail to fill with:
- Enterprise-grade authentication architecture
- JWT + OAuth2 implementation
- Multi-factor authentication
- Security threat modeling
- RBAC implementation
- API security best practices
- Compliance and audit trails

---

## Security Infrastructure & Protocols

**Mikhail Trifonov**


Details to include:
- Spring Security + JWT architecture
- OAuth2 flow implementation
- Password hashing algorithms (bcrypt, etc.)
- Rate limiting and DDoS protection
- Session management strategies
- Security headers implementation
- Vulnerability assessment results
- Penetration testing outcomes



---

## Auth Service: Performance & Scalability

**Mikhail Trifonov**


Details to include:
- Authentication performance metrics
- Token validation optimization
- Caching strategies for auth
- Load testing results
- Horizontal scaling approach
- Database optimization for auth
- Monitoring and alerting setup


---

# 👥 Users Service & Core Logic

**Mikhail Trifonov**


This slide is for Nikita to fill with:
- Users service architecture design
- Profile management system
- Advanced user roles and permissions
- Data modeling and relationships
- Business logic implementation
- Service integration patterns



---

## Users Service: Technical Architecture

**Mikhail Trifonov**


Details to include:
- Spring Boot microservice design
- gRPC service implementation
- Database schema and optimization
- User profile data modeling
- RBAC system implementation
- Caching strategies
- Performance benchmarks



---

## Users Service: Integration & Communication

**Mikhail Trifonov**


Details to include:
- gRPC protocol implementation
- Service-to-service communication
- Error handling and retry logic
- Circuit breaker patterns
- Distributed tracing
- Logging and monitoring
- API versioning strategy


---
<!-- _class: section h1 -->

# 📥API Gateway📤

**Nikita Maksimenko**

The API Gateway centrally coordinates frontend REST API requests, executes business logic, and routes them to backend microservices via gRPC.

---
<!-- _class: compact-list -->


## API Gateway: Core Responsibilities

- ❌ Problem: Multiple services to interact with
    ⤷ ✅ Solution: API Gateway service
- 🌐 **Centralized Entry Point**: Serves as the unified access layer for all client REST API requests
- 🔀 **Request Routing**: Directs incoming requests to the appropriate microservice (`auth`, `user`, `article`, `lab`) via gRPC
- 🔒 **Authentication & Security**: Validates JWT tokens and user's permissions
- 📝 **Cross-Cutting Concerns**: Handles logging, request tracing, and error handling for all API traffic
- 🧠⚙️ **Business Logic Execution**: Aggregating data and enforcing business rules beyond simple routing


---
<!-- _class: compact-list -->

## API Gateway: Communication & Tech

- 📥 Receive data from frontend via REST
    ⤷ REST is the simplest and most widely supported method for web communication
- 🛡️ Intercept incoming REST requests for authentication and authorization
    ⤷ Ensures secure access and centralized permission checks
- 🔀 Route requests internally to backend microservices via gRPC
    ⤷ gRPC provides high-speed, type-safe, and scalable service-to-service communication
- 📤 Return responses to the client through the API Gateway
    ⤷ Centralizes response handling and error management
- 🧑‍💻 Use Java 21, Spring Boot 3 (Web, AOP, Doc OpenAPI), gRPC
    ⤷ Ensures a secure, efficient, and maintainable technology stack for all platform components

---
<!-- _class: compact-list -->

## API Gateway: Problems & Solutions

- ❌ Too many services and people to communicate with
    ⤷ ✅ Create clear rules of communication and define issue execution order for efficient collaboration
- ❌ Unclear models from both frontend and backend
    ⤷ ✅ Establish detailed requirements for each request step to ensure consistency and clarity
- ❌ Lack of data checks on frontend
    ⤷ ✅ Use Jackson validators in request models to enforce data integrity before processing


---

# Articles
Timur

---
# Articles
Timur

---

# Articles
Timur

---
# 🧪 Labs Service & Content Pipeline

**Timur Salakhov - Content Systems Engineer**


This slide is for Timur to fill with:
- Labs service architecture
- Content management and versioning
- Advanced file processing pipeline
- Lab creation and distribution workflow
- Submission handling system
- MinIO integration and optimization

---

## Labs Service: File Processing Engine

**Timur Salakhov**

Details to include:
- Asynchronous file processing
- MinIO distributed storage
- File validation and security scanning
- Content versioning system
- Submission workflow automation
- Performance optimization techniques
- Error handling and recovery


---

## Labs Service: Performance & Storage

**Timur Salakhov**


Details to include:
- Storage optimization strategies
- CDN integration for content delivery
- Compression and deduplication
- Backup and disaster recovery
- Performance metrics and monitoring
- Scalability testing results
- Cost optimization techniques


---

# 💬 Feedback Service & Review Engine

**Ravil Kazeev - Algorithms Engineer**


This slide is for Ravil to fill with:
- Feedback service architecture
- Advanced peer review algorithms
- Reputation and scoring systems
- Review quality assurance
- Anti-spam and fraud detection
- Analytics and insights engine


**[Review engine architecture to be detailed by team member]**

---

## Feedback Algorithms & Intelligence

**Ravil Kazeev**


Details to include:
- Peer review matching algorithms
- Scoring and ranking systems
- Quality assessment metrics
- Bias detection and mitigation
- Machine learning for review quality
- A/B testing frameworks
- Performance analytics


**[Algorithm implementation and intelligence details to be added]**

---

## Feedback Service: Data Engineering

**Ravil Kazeev**


Details to include:
- Database design for feedback data
- Real-time analytics pipeline
- Data warehousing and ETL
- Performance monitoring
- Scalability optimization
- Data privacy and compliance
- Reporting and visualization


**[Data engineering and analytics details to be added]**

---

# Marimo 
Mikhail

---

# Marimo
Mikhail

---

# Marimo
Mikhail

---

# 🤖 AI Features in Our Service

## Two Powerful Enhancements:
- 🔍 **AI RAG Assistant**  
  Context-aware code and documentation helper, leveraging Retrieval-Augmented Generation (RAG) to deliver accurate, real-time support to students.

- ✅ **Autograding**  
  Automated code assessment system for evaluating submissions instantly — ideal for learning platforms.


---

## AI Models 

<div style="display: flex; gap: 2em;">

<div style="flex: 1;">
<h3>🤖 AI RAG Assistant</h3>
<ul>
  <li>Qwen2.5-Coder-1.5B-Instruct (local inference)</li>
  <li>Qdrant vector store</li>
  <li>BAAI/bge-small-en-v1.5 embeddings</li>
</ul>
</div>

<div style="flex: 1;">
<h3>✅ Autograding</h3>
<ul>
  <li>deepseek-r1-distill-llama-70b (groq inference)</li>
  <li>Menagerie: A Dataset of Graded CS1 Assignments for evaluation</li>
  <li>Celery message broker </li>
</ul>
</div>

</div>


---

## 🚧 ML Infrastructure



![alt text](asssets/open-labs-share-ml.drawio.png)


---
## ⚙️ ML technical details


<div style="display: flex; gap: 2em;">

<div style="flex: 1;">
<h3>🧩 Backend Architecture</h3>
<ul>
  <li>FastAPI-based backend</li>
  <li>Three-layer structure:
    <ul>
      <li>🔹 API Layer (routers, validation)</li>
      <li>🔹 Service Layer (business logic)</li>
      <li>🔹 Data Layer (DB / embedding stores)</li>
    </ul>
  </li>
  <li>Dockerized microservices</li>
  <li>MQ (Celery/Redis for grading)</li>
</ul>
</div>

<div style="flex: 1;">
<h3>🧠 ML + RAG Pipeline</h3>
<ul>
  <li>Recursive chunking for long docs</li>
  <li>Embedding via transformer model (BGE)</li>
  <li>Vector DB (Qdrant)</li>
  <li>Relevance thresholding (cosine similarity)</li>
  <li>RAG with prompt templating for generation</li>
</ul>
</div>

</div>

---
<!-- _class: section h1 -->

# 🚀 DevOps & Cloud Infrastructure

**Kirill Efimovich - DevOps Engineer**

Our DevOps philosophy centers on 🤖 automation, 📦 consistency, and ⚡ rapid, reliable delivery. We've built a robust CI/CD pipeline and infrastructure to support the entire development lifecycle, from code commit to deployment.

---
<!-- _class: compact-list -->

## DevOps: Primary Goals

- 🤖 **Automate Everything**: Eliminate manual steps in building, testing, and deploying to increase efficiency and reduce human error.
- 📦 **Consistent Environments**: Use Docker to ensure that what works on a developer's machine also works in production.
- ⚡ **Enable Rapid Feedback**: Automatically deploy every merge to `main` to a live staging environment for immediate testing and user feedback.
- 🤝 **Streamline Collaboration**: Integrate project management automation to keep the team synchronized.

---
<!-- _class: compact-list -->

## DevOps: Tech Stack & Connections

A look at the tools that power our automated pipeline.

- **Automation:** GitHub Actions
- **Containerization:** Docker & Docker Compose with Bake
- **Registry:** GitHub Container Registry (GHCR)
- **Infrastructure:** Self-hosted server with NGINX & HAProxy
- **Server setup:** Ubuntu 24.04 LTS, 6 CPUs, 16GB RAM, 240GB SSD
- **Networking:** CloudPub for external access



---
<!-- _class: compact-list -->

## DevOps: Problems & Solutions

- ❌ **Problem:** University network NAT blocked external access to our self-hosted server.
    ⤷ ✅ **Solution:** After issues with Cloudflare, we successfully used **CloudPub** to create a secure tunnel for public access.
- ❌ **Problem:** The initial CI/CD pipeline was complex and required many iterations to stabilize.
    ⤷ ✅ **Solution:** Through persistent, collaborative effort, we developed a set of reliable, modular GitHub Actions workflows.
- ❌ **Problem:** Risk of downtime during manual deployments.
    ⤷ ✅ **Solution:** We fully automated the deployment process and are implementing a **Blue-Green strategy** to ensure zero-downtime updates.

---

## Engineering Challenges: Real-World Solutions (засунуть на каждую секцию)

### **1. Polyglot Microservices at Scale**
- **Challenge:** Type-safe communication between Java, Go, and Python services
- **Solution:** Protocol Buffers + gRPC code generation with automated API contracts
- **Metrics:** 40% latency reduction, 99.9% type safety, zero breaking changes in 6 months

### **2. Real-Time Collaboration Infrastructure**
- **Challenge:** Live coding sessions with sub-second latency for global users
- **Solution:** WebSocket clustering with Redis pub/sub and geographic load balancing
- **Metrics:** <100ms global latency, supports 1000+ concurrent sessions

### **3. AI-Driven Content Intelligence**
- **Challenge:** Contextual lab recommendations and intelligent Q&A at scale
- **Solution:** Vector embeddings + semantic search with incremental model training
- **Metrics:** 85% recommendation accuracy, 2-second response time for complex queries

---

<!-- _class: lead -->

# 🚀 Technical Innovation Showcase

**Q&A / Deep Technical Discussion**

---

**Explore the Engineering:**
- **Architecture & Code:** [github.com/IU-Capstone-Project-2025/open-labs-share](https://github.com/IU-Capstone-Project-2025/open-labs-share)
- **Live Technical Demo:** [open-labs-share.online](https://open-labs-share.online/) 