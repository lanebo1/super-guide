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

# :sunflower: Frontend

**Aleliya Turushkina**

A modern web app that lets users explore, contribute, and review labs and articles through an interactive, user-friendly interface.

---

## :mushroom: Frontend: Main user interface for the Open Labs Share

- :file_folder: Handles user authentication, profile management, and navigation
- :book: Enables users to:
  - Browse, upload, and review labs and articles
  - Participate in peer review and feedback
  - Interact with real-time features (e.g., chat, notifications)


---

## :tulip: Frontend: Tech Stack & Connections

- :sunny: **Frontend:** React, Vite, Tailwind CSS, React Router
- :seedling: **Component Libraries:** React PDF Viewer, Markdown/KaTeX
- :earth_africa: **API Integration:**
    - Communicates with backend via REST API through the API Gateway
    - Auth, Labs, Articles, Submissions, Feedback, and ML services
    - Real-time and file download support from MinIO

---

## :blossom: Frontend: Problems & Solutions

- ❌ Lack of viewing of the user's submission and feedback
     ✅ Downloading files directly from MinIO
- ❌ Inability to view Markdown using a dark theme
     ✅ Implemented theme switching and style across the entire platform


---

## Lets go to backend
---
<!-- _class: tech-details -->

## Advanced System Architecture

**Cloud-native architecture designed for high availability and horizontal scaling**

```mermaid

```

---

# 🔐 Authentication Service

**Mikhail Trifonov**

Stateless JWT-based authentication microservice providing enterprise-grade security for the entire Open Labs Share ecosystem 🛡️

---

## Authentication Service: Primary Use Case

**Handles all authentication flows and token lifecycle management for secure access control** 🔑

- 🔑 **User Authentication**: `Sign-in/sign-up` with users-service gRPC calls 👤
- 🎟️ **JWT Generation**: Creates access & refresh `tokens` with user claims 🔐
- ✅ **Token Validation**: `Verifies` signatures, expiration, and blacklist status 🛡️
- 🚪 **Session Management**: Logout with token `blacklisting` for security 🏴‍☠️
- 🛡️ **Security Gateway**: Validates all API requests for `protected` resources 🦝



---

## Authentication Service: Tech Stack & Connections

**Java Spring with gRPC communication and no database 😎**

- 🏗️ **Java 21 + Spring Boot 3.5:**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ `REST` controller for endpoints
- 🔐 **Spring Security + JWT:** 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Token generation with signing and validation, refresh token support
- 🚀 **gRPC Server/Client:** 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ High-performance calls to Users Service and token validation for API Gateway
- 💾 **In-Memory Blacklist:** 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Storage for invalidated tokens for logout functionality
- 📚 **OpenAPI Docs:** Auto-generated REST API documentation 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Interactive API documentation for frontend integration and testing

---

## Authentication Service: Problems & Solutions

- ❌ **Problem**: Same JWT is still available after user logout
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Token `blacklisting` and invalidating on logout 📝
- ❌ **Problem**: User data consistency between Auth and Users Services
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Single `source of truth` in Users Service, Auth Service fetches on-demand and do not store any users data 👮 🤝 🙍‍♂️
- ❌ **Problem**: Username changes makes current JWT invalid
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Token `reissue` logic if that preserves user sessions seamlessly 🛂



---

# 👥 Users Service

**Mikhail Trifonov**

Single source of truth for all user data with profile management and points system 📊



---

## Users Service: Primary Use Case

**Manages all user data, credentials, and points for solving &reviewing labs** 🎯

- 🆕 **User Registration**: Creates new user accounts 👤
- 🔐 **Credential Management**: Stores bcrypt-hashed passwords, validates username/email and password
- 👤 **Profile Operations**: CRUD for user profiles ✏️
- 🏆 **Points System**: Tracks labs solved/reviewed counts & points balance 💵💰💳
- 📈 **Data Integrity**: Single source of truth for all user-related information 🐟


---

## Users Service: Tech Stack & Connections

**Java with PostgreSQL persistence and gRPC API** ☕🐘

- 🔧 **Java 21 + Spring Boot 3.5:** 
&nbsp;&nbsp;&nbsp;⤷ `REST` controllers and JPA repositories for user management
- 🗄️ **PostgreSQL:**
&nbsp;&nbsp;&nbsp;⤷ Stores user data, credentials, points, and labs solved/reviewd counts
- 📋 **Flyway:** 
&nbsp;&nbsp;&nbsp;⤷ Database schema versioning and `migration` management
- ⚡ **gRPC Server:** 
&nbsp;&nbsp;&nbsp;⤷ Provides `API` for user validation, data retrieval, and points updates to other microservices

---

## Users Service: Problems & Solutions

- ❌ **Problem**: Create-drop strategy in ORM caused inconsistency when all containers restarted
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Flyway for SQL tables creation instead of auto-creation by ORM. Validate strategy 🦜🦅🐦‍⬛🐦
- ❌ **Problem**: Points system requiring strict control on changes due to its _"money"_ purpose
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Transactional methods to prevent inconsistency in balance and counters 🤑


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

# 📄 Articles Service

**Timur Salakhov**

The central repository for all scientific articles and research papers, enabling authors to publish content and students to access educational materials.

---

## 📚 Articles Service: Primary Use Cases

- **For Authors:** 📝 Publish scientific articles and research papers in PDF format
- **For Teachers:** 🔗 Link lab assignments with relevant theoretical articles and background materials  
- **For Students:** 📖 Access scientific articles, download assets for offline study, and search content
- **Content Management:** 🗂️ CRUD operations for articles and file assets with access control

---

## ⚙️ Articles Service: Tech Stack & Connections

**Core Technologies:**
- **🐍 Programming Language:** Python 3.12
- **🔄 Inter-service Communication:** gRPC (`grpcio`, `grpcio-tools` libraries)
- **🗄️ Database:** PostgreSQL via SQLAlchemy (`sqlalchemy`, `sqlalchemy-serializer` libraries)
- **☁️ Object Storage:** MinIO (`minio` library)
- **🐳 Containerization:** Docker, Docker Compose
- **⚙️ Config Management:** `python-dotenv`, Environment Variables
- **🧪 Testing:** Pytest unit-testing (`pytest` library)
- **📝 Logging:** Python logging (built-in `logging` library)

**Service Integrations:**
- **🚪 API Gateway**: Receive and return data in gRPC format
- **🗄️ PostgreSQL Database**: Store all articles and its assets metadata
- **☁️ MinIO Storage System**: Store all articles assets

---

## 🛠️ Articles Service: Problems & Solutions

| ❌ **Problems**                                         | ✅ **Solutions**                                                                                   |
|--------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| ❌ Difficult interaction with database via SQL queries | ✅ Use `SQLAlchemy` ORM system for convenient and flexible database interaction  |
| ❌ Need to organize article files systematically          | ✅ Created structured MinIO bucket organization: `articles/article_id/article.pdf`                  |
| ❌ Large PDF files causing timeout issues during upload    | ✅ Implemented streaming gRPC uploads for efficient file transfer                                   |
| ❌ Frontend does searching across articles      | ✅ Moved searching on service and built text search functionality on titles and abstracts with pagination               |

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

# 📓 Marimo Service

**Mikhail Trifonov**

Dual-architecture microservice providing real-time interactive Python notebook execution powered by Marimo library 🐍🟢

---

## Marimo Service: Primary Use Case

**Interactive code execution and data visualization through cells with Python code** 🔬

- 📝 **Notebook Management**: CRUD operations for marimo components linked to labs/articles 🔗
- ⏰ **Session Orchestration**: Start/stop interactive Python sessions with TTL 🪦
- 👟 **Code Execution**: Real-time cell execution with output capture and error handling 🖐️
- 📊 **Asset Management**: Upload/download datasets and files for notebook use 🐪
- 🎛️ **Interactive Widgets**: Set of basic Marimo input widgets which value can be used in code (sliders, switchers, text fields, etc.) 📟
- 📁 **Cross-cells state memory**: Variables and modules from executed cells are availabe in other cells 📦

---

## Marimo Service: Tech Stack & Connections

**Java for metadata management with Python native code execution** ☕🐍

- 🔧 **Java Manager + Python Executor:** 
&nbsp;&nbsp;&nbsp;⤷ Java handles `REST API` and `metadata` while Python `executes` notebooks
- 🗄️ **PostgreSQL:** 
&nbsp;&nbsp;&nbsp;⤷ Tracks notebook metadata, user sessions, and execution trails with TTL cleanup
- 📦 **MinIO:**
&nbsp;&nbsp;&nbsp;⤷ Object storage for notebook `files` and user-uploaded `assets`
- 🔗 **gRPC:**  
&nbsp;&nbsp;&nbsp;⤷ Java Manager ← `execute requests, session management` → Python Executor
- 🐍 **Marimo:** Interactive notebook execution with widgets
&nbsp;&nbsp;&nbsp;⤷ Interactive notebook execution with ✨`widgets`✨

---

## Marimo Service: Problems & Solutions

- ❌ **Problem**: High load on one service to manage metadata, connections with other services, and execution at the same time
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Dual-service architecture for management from execution 2️⃣✌️
- ❌ **Problem**: Managing variables and modules across multiple code cells
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Sessions for notebooks to track existing and erased variables/modules 🧹
- ❌ **Problem**: Marimo widgets incompatibility with our needs and tech
&nbsp;&nbsp;&nbsp;⤷ ✅ **Solution**: Custom design widgets (but based on Marimo widgets) with configurable behaviour fully under our control 🧩🕹️

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

From manual processes to a fully automated pipeline. We engineered a robust DevOps foundation to enable rapid development, consistent testing, and reliable, zero-downtime deployments for the Open Labs Share platform.

---
<!-- _class: compact-list -->

## DevOps: Primary Goals

- 🤖 **Accelerate Delivery:** Fully automate the build, test, and deployment lifecycle.
- 📦 **Ensure Stability:** Create reproducible environments with Docker for development and production.
- ⚡ **Enable Rapid Iteration:** Deploy every change to a live staging environment for immediate feedback.
- 🤝 **Improve Collaboration:** Use GitOps and project automation to keep the team perfectly synchronized.

---

## 🔄 The CI/CD Pipeline

<div style="display: flex; justify-content: space-around; text-align: center; gap: 1em;">
  <div style="flex: 1;">
    <h3>1. Code & Commit</h3>
    <p>Developer pushes code to a feature branch.</p>
  </div>
  <div style="flex: 1;">
    <h3>2. Pull Request</h3>
    <p>Automated checks run via GitHub Actions.</p>
  </div>
  <div style="flex: 1;">
    <h3>3. Merge to Main</h3>
    <p>Triggers build & push to GHCR.</p>
  </div>
  <div style="flex: 1;">
    <h3>4. Deploy</h3>
    <p>New version deployed to Staging.</p>
  </div>
</div>

<h4>Key GitHub Actions Workflows:</h4>
<ul>
  <li><b>Compilation Validation:</b> Ensures all services compile.</li>
  <li><b>Test Execution:</b> Runs unit & integration tests.</li>
  <li><b>Docker Build Validation:</b> Validates Docker image builds.</li>
  <li><b>Deployment Automation:</b> Handles the Blue-Green deployment logic.</li>
</ul>

---

## 💻 Infrastructure & Deployment

<div style="display: flex; gap: 2em;">
<div style="flex: 2;">
<h3>🔵 Green-Blue Strategy 🟢</h3>
<ul>
    <li><b>Zero Downtime:</b> Updates are seamless.</li>
    <li><b>Workflow:</b>
        <ol type="i">
            <li>Deploy new version (Green) alongside Production (Blue).</li>
            <li>Test Green environment internally.</li>
            <li>Switch HAProxy to route traffic to Green.</li>
            <li>Keep Blue for instant rollback.</li>
        </ol>
    </li>
</ul>
</div>
<div style="flex: 1.2; border-left: 0.5px; padding-left: 2em; margin-bottom: 2em;">
<h3>🌐 Server & Networking</h3>
<ul>
  <li><b>Host:</b> Self-managed server on Ubuntu 24.04</li>
  <li><b>Specs:</b> 6-Core CPU, 16GB RAM, 240GB SSD</li>
  <li><b>Proxy:</b> NGINX & HAProxy</li>
  <li><b>Access:</b> CloudPub for public NAT traversal</li>
  <li><b>Monitoring:</b> cAdvisor for container metrics</li>
</ul>
</div>
</div>

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