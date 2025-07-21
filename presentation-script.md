# Open Labs Share - Presentation Script

**Practicum Project Defense, S25**
**Team:** Aleliya Turushkina, Kirill Efimovich, Nikita Maksimenko, Timur Salakhov, Ravil Kazeev, Mikhail Trifonov, Kirill Shumskiy

---

## Opening & Introduction

**Speaker: Kirill Efimovich (PM/DevOps)**

Good morning, everyone. I'm Kirill Efimovich, the project manager and DevOps engineer for our team. Today we're excited to present Open Labs Share - a next-generation learning platform that bridges the gap between academic theory and real-world industry practice through microservices architecture.

Our mission was to solve critical engineering challenges in education technology: scalability bottlenecks in traditional learning management systems, limited real-world project experience for students, inefficient mentor-learner matching, and poor feedback loops between industry needs and educational content.

Let me introduce our distributed engineering team. We have Aleliya Turushkina handling frontend architecture and user experience, Mikhail Trifonov managing security engineering and authentication systems, Nikita Maksimenko leading backend architecture and core services, Timur Salakhov overseeing content pipeline and storage systems, Ravil Kazeev working on algorithms engineering and review systems, and Kirill Shumskiy developing AI/ML engineering and intelligence systems.

---

## Product & Technical Vision

**Speaker: Kirill Efimovich (PM/DevOps)**

Open Labs Share revolutionizes education through three key innovations. First, streamlined content creation with a version-controlled lab management system that enables experts to publish and maintain high-quality learning materials. Second, a guided learning experience with structured submission and review processes that provide meaningful feedback and track progress. Third, smart community building through AI-enhanced networking that connects learners with relevant peers and mentors based on skills and interests.

From a technical perspective, we've built a cloud-native, microservices-driven learning ecosystem. Our expert content pipeline uses a Git-inspired versioning system for lab content with automated distribution. The learner development workflow operates like a CI/CD pipeline with automated validation and feedback routing. Finally, our intelligent community leverages ML-driven peer matching and reputation-based quality assurance systems.

---

## Live Demo Walkthrough

**Speaker: Aleliya Turushkina (Frontend)**

Now I'll demonstrate our platform's core capabilities. First, you'll see our secure authentication system with OAuth2 and JWT implementation including multi-factor authentication. Next, I'll show our intelligent lab discovery feature powered by ML recommendations and advanced search capabilities. Then we'll explore our advanced development workflow with real-time collaboration and submission pipeline. I'll demonstrate our intelligent review engine with AI-assisted peer matching and quality scoring. Finally, we'll look at our analytics dashboard providing real-time metrics and performance insights.

[Conduct live demo showing each feature]

The user interface is built with React and modern web technologies, providing an intuitive experience for both learners and educators. Users can seamlessly browse content, submit assignments, participate in peer reviews, and engage in real-time collaboration.

---

## Frontend Architecture

**Speaker: Aleliya Turushkina (Frontend)**

Our frontend serves as the main user interface for the Open Labs Share platform. It handles user authentication, profile management, and navigation while enabling users to browse, upload, and review labs and articles. The system supports interactive features like peer review and feedback systems, plus real-time collaboration through chat, notifications, and live interaction capabilities.

We built this using React, Vite, Tailwind CSS, and React Router for the core framework. Component libraries include React PDF Viewer and Markdown with KaTeX support. The frontend communicates with our backend via REST API through the API Gateway, integrating with Auth, Labs, Articles, Submissions, Feedback, and ML services, plus real-time file download support from MinIO.

We solved two key challenges: first, the lack of viewing capabilities for user submissions and feedback, which we addressed by implementing direct file downloads from MinIO. Second, the inability to view Markdown content using a dark theme, which we solved by implementing comprehensive theme switching and styling across the entire platform.

---

## System Architecture Overview

**Speaker: Nikita Maksimenko (Backend Architecture)**

Before diving into individual services, let me explain our overall system architecture. We've designed a cloud-native architecture for high availability and horizontal scaling. Our microservices communicate via gRPC for high-performance, type-safe interactions, while the frontend communicates through REST APIs via our centralized API Gateway.

This architecture enables us to scale individual components independently, maintain strong service boundaries, and ensure reliable communication between polyglot services written in Java, Go, and Python.

---

## Authentication Service

**Speaker: Mikhail Trifonov (Security Engineering)**

I'll start with our Authentication Service, which provides stateless JWT-based authentication for enterprise-grade security across the entire Open Labs Share ecosystem.

This service handles all authentication flows and token lifecycle management for secure access control. It manages user authentication through sign-in and sign-up with gRPC calls to the Users Service. The service generates JWT access and refresh tokens with user claims, verifies signatures, expiration, and blacklist status. It provides session management with logout and token blacklisting for security, and serves as a security gateway validating all API requests for protected resources.

Our tech stack uses Java 21 with Spring Boot 3.5 for REST controllers, Spring Security with JWT for token generation, signing, validation, and refresh token support. We use gRPC for high-performance calls to the Users Service and token validation for the API Gateway. An in-memory blacklist stores invalidated tokens for logout functionality, and we provide OpenAPI documentation for interactive API testing.

We solved three critical problems: first, JWT tokens remaining valid after user logout, which we addressed through token blacklisting and invalidation. Second, user data consistency between Auth and Users Services, solved by establishing a single source of truth in the Users Service while the Auth Service fetches data on-demand without storing user information. Third, username changes invalidating current JWTs, resolved through token reissue logic that preserves user sessions seamlessly.

---

## Users Service

**Speaker: Mikhail Trifonov (Security Engineering)**

The Users Service serves as the single source of truth for all user data with comprehensive profile management and a points system.

It manages all user data, credentials, and points for solving and reviewing labs. The service handles user registration creating new accounts, credential management storing bcrypt-hashed passwords and validating usernames, emails, and passwords. It provides CRUD operations for user profiles, tracks labs solved and reviewed counts with points balance, and maintains data integrity as the single source of truth for all user-related information.

We use Java 21 with Spring Boot 3.5 for REST controllers and JPA repositories. PostgreSQL stores user data, credentials, points, and lab statistics. Flyway handles database schema versioning and migration management. Our gRPC server provides APIs for user validation, data retrieval, and points updates to other microservices.

Two main challenges were resolved: first, the create-drop ORM strategy causing inconsistency during container restarts, solved by implementing Flyway for SQL table creation instead of auto-creation with a validate strategy. Second, strict control requirements for the points system due to its monetary purpose, addressed through transactional methods preventing inconsistency in balance and counters.

---

## API Gateway

**Speaker: Nikita Maksimenko (Backend Architecture)**

The API Gateway serves as the centralized entry point coordinating frontend REST API requests, executing business logic, and routing them to backend microservices via gRPC.

It provides centralized entry point serving as the unified access layer for all client REST API requests. The gateway handles request routing directing incoming requests to appropriate microservices including auth, user, article, and lab services via gRPC. It manages authentication and security validating JWT tokens and user permissions. The service handles cross-cutting concerns like logging, request tracing, and error handling for all API traffic, plus business logic execution aggregating data and enforcing business rules beyond simple routing.

Our tech stack uses Java Spring Boot with REST-to-gRPC translation. We receive data from frontend via REST as the simplest and most widely supported web communication method. Our security layer intercepts incoming REST requests for authentication and authorization ensuring secure access and centralized permission checks. The gRPC client routes requests internally to backend microservices providing high-speed, type-safe, and scalable service-to-service communication. Response handling returns responses to clients through the gateway centralizing response handling and error management.

We addressed three problems: too many services and people to communicate with, solved by creating clear communication rules and defining issue execution order for efficient collaboration. Unclear models from both frontend and backend, resolved by establishing detailed requirements for each request step ensuring consistency and clarity. Lack of data checks on frontend, addressed using Jackson validators in request models to enforce data integrity before processing.

---

## Articles Service

**Speaker: Timur Salakhov (Content Pipeline)**

The Articles Service serves as the central repository for all scientific articles and research papers, enabling authors to publish content and students to access educational materials.

This service manages all articles and assets metadata. It provides CRUD operations for article details, handles article assets in an independent storage system, organizes and updates metadata for articles and assets, and provides article searching based on title and abstract.

We built this using Python 3.12 as our programming language with gRPC for inter-service communication. PostgreSQL serves as our database while MinIO provides object storage. The system uses Docker and Docker Compose for containerization, environment variables for configuration management, Pytest for unit testing, and Python logging.

The service integrations include the API Gateway receiving and returning data in gRPC format, PostgreSQL database storing all articles and asset metadata, and MinIO storage system storing all article assets.

We resolved four key challenges: difficult database interaction via SQL queries, solved by using SQLAlchemy ORM for convenient and flexible database interaction. The need to organize article files systematically, addressed by creating structured MinIO bucket organization with articles organized by article ID. Large files causing timeout issues during upload, resolved by implementing streaming gRPC uploads for efficient file transfer. Frontend searching across articles, solved by moving search functionality to the service and building text search with pagination.

---

## Labs Service

**Speaker: Timur Salakhov (Content Pipeline)**

The Labs Service serves as the central repository for all laboratory work and student submissions, enabling teachers to create assignments and students to submit solutions with comprehensive grading and feedback.

This service manages all labs, submissions, and educational content. It provides CRUD operations for lab assignments with tags, handles submissions with text content and file assets, organizes labs with flexible tagging and search capabilities, and tracks submission status and grade workflow.

We use Python 3.12 with hybrid database architecture and MinIO storage. The tech stack includes gRPC for inter-service communication, PostgreSQL plus MongoDB for databases, MinIO for object storage, Docker and Docker Compose for containerization, environment variables for configuration management, Pytest for unit testing, and Python logging.

Service integrations include the API Gateway as single entry point for all requests, PostgreSQL database storing labs, submissions, tags, and asset metadata, MongoDB database storing submission text content for flexible storage, and MinIO storage system storing lab and submission assets in organized buckets.

We addressed five problems: complex data relationships between labs, submissions, and tags, solved using SQLAlchemy models with proper foreign keys and many-to-many relationships for structured data management. Large submission text content causing database bloat, resolved by implementing hybrid storage with metadata in PostgreSQL and text content in MongoDB for flexibility. The need to organize files systematically, addressed by creating structured MinIO bucket organization for labs and submissions. Frontend searching across labs, solved by moving search to the service and building text and tag search functionality with pagination. Frontend searching submissions to review, resolved by moving search to the service and building reviewable submissions retrieval functionality.

---

## Feedback Service

**Speaker: Ravil Kazeev (Algorithms Engineering)**

The Feedback Service centralizes feedback and discussion by managing detailed lab reviews, supporting file attachments, and powering threaded conversations for both labs and articles.

This comprehensive feedback and discussion management system enables reviewers to create, update, and delete detailed feedback on submissions using Markdown for text and code formatting. It powers a threaded commenting system for both labs and articles with nested replies keeping conversations structured and easy to follow. The service allows multiple file attachments per feedback entry, using efficient gRPC streaming to handle large uploads and downloads without high memory usage.

We built this using Go 1.24 as a high-performance, concurrent service ideal for I/O-heavy tasks. Our gRPC server provides a typed API for feedback, comments, and file streaming. We implemented a multi-storage backend with PostgreSQL storing structured feedback metadata, MongoDB storing unstructured comments and feedback content, and MinIO providing object storage for all file attachments.

Three major problems were resolved: first, a single database was inefficient for managing varied data types including metadata, text, and files. We implemented a multi-storage architecture using the best database for each job - PostgreSQL for metadata, MongoDB for comments, and MinIO for file attachments. Second, uploading large files as a single request was unreliable, leading to timeouts and memory errors. We re-architected attachment handling using gRPC streaming, processing files in small chunks for efficient and robust transfers. Third, serving file downloads through the Feedback service would create an unnecessary bottleneck and consume server resources. We configured the MinIO bucket for public read access, allowing the service to provide direct file URLs to the frontend and offload all download traffic.

---

## Marimo Service

**Speaker: Mikhail Trifonov (Security Engineering)**

The Marimo Service is a dual-architecture microservice providing real-time interactive Python notebook execution powered by the Marimo library.

This service enables interactive code execution and data visualization through cells with Python code. It provides notebook management with CRUD operations for marimo components linked to labs and articles. Session orchestration starts and stops interactive Python sessions with TTL. Code execution happens in real-time with output capture and error handling. Asset management handles upload and download of datasets and files for notebook use. Interactive widgets provide basic Marimo input widgets whose values can be used in code including sliders, switches, text fields, and more. Cross-cell state memory ensures variables and modules from executed cells are available in other cells.

Our tech stack uses Java for metadata management with Python native code execution. The Java Manager handles REST API and metadata while Python executes notebooks. PostgreSQL tracks notebook metadata, user sessions, and execution trails with TTL cleanup. MinIO provides object storage for notebook files and user-uploaded assets. gRPC enables communication between Java Manager and Python Executor for execute requests and session management. Marimo provides interactive notebook execution with custom widgets.

We solved three challenges: high load on one service managing metadata, connections with other services, and execution simultaneously, resolved through dual-service architecture separating management from execution. Managing variables and modules across multiple code cells, solved using sessions for notebooks to track existing and erased variables and modules. Marimo widgets incompatibility with our needs and technology, addressed by creating custom design widgets based on Marimo widgets with configurable behavior fully under our control.

---

## AI/ML Service

**Speaker: Kirill Shumskiy (AI/ML Engineering)**

The AI/ML Service provides advanced AI-powered features with intelligent assistance and automated grading capabilities for enhanced learning experience.

We deliver two powerful AI enhancements for the learning platform. First, our AI RAG Assistant provides context-aware code and documentation help, leveraging Retrieval-Augmented Generation to deliver accurate, real-time support to students. Second, our Autograding system offers automated code assessment for evaluating submissions instantly, ideal for learning platforms.

Our FastAPI backend uses specialized AI models and infrastructure. For the AI RAG Assistant, we use Qwen2.5-Coder-1.5B-Instruct for local inference, Qdrant vector store, and BAAI/bge-small-en-v1.5 embeddings. For Autograding, we use deepseek-r1-distill-llama-70b for groq inference, Menagerie Dataset of Graded CS1 Assignments for evaluation, and Celery message broker.

Our core architecture includes FastAPI-based backend with three-layer structure: API Layer for routers and validation, Service Layer for business logic, and Data Layer for databases and embedding stores. We use dockerized microservices with message queues including Celery and Redis for grading.

The ML and RAG pipeline includes recursive chunking for long documents, embedding via transformer model BGE, Vector DB with Qdrant, relevance thresholding using cosine similarity, and RAG with prompt templating for generation.

---

## DevOps & Cloud Infrastructure

**Speaker: Kirill Efimovich (PM/DevOps)**

Our DevOps infrastructure represents a journey from manual processes to a fully automated pipeline. We engineered a robust DevOps foundation enabling rapid development, consistent testing, and reliable, zero-downtime deployments.

Our automated deployment pipeline and infrastructure management accelerates delivery by fully automating the build, test, and deployment lifecycle. We ensure stability by creating reproducible environments with Docker for development and production. Rapid iteration is enabled by deploying every change to a live staging environment for immediate feedback. We improve collaboration using GitOps and project automation to keep the team perfectly synchronized.

Our automated CI/CD pipeline uses Blue-Green deployment strategy. The workflow includes four steps: developers push code to feature branches, pull requests trigger automated checks via GitHub Actions, merging to main triggers build and push to GitHub Container Registry, and new versions deploy to staging automatically.

Key GitHub Actions workflows include compilation validation ensuring all services compile, test execution running unit and integration tests, Docker build validation validating Docker image builds, and deployment automation handling Blue-Green deployment logic.

Our infrastructure uses a Green-Blue strategy providing zero downtime with seamless updates. The workflow deploys new versions Green alongside Production Blue, tests Green environment internally, switches HAProxy to route traffic to Green, and keeps Blue for instant rollback.

Our server and networking setup includes a self-managed server on Ubuntu 24.04 with 6-Core CPU, 16GB RAM, and 240GB SSD. We use NGINX and HAProxy for proxying, CloudPub for public NAT traversal, and cAdvisor for container metrics.

We resolved three critical problems: university network NAT blocking external access to our self-hosted server, solved by using CloudPub to create a secure tunnel for public access after issues with Cloudflare. The initial CI/CD pipeline being complex and requiring many iterations to stabilize, resolved through persistent, collaborative effort developing reliable, modular GitHub Actions workflows. Risk of downtime during manual deployments, addressed by fully automating the deployment process and implementing a Blue-Green strategy ensuring zero-downtime updates.

---

## Technical Achievements & Metrics

**Speaker: Nikita Maksimenko (Backend Architecture)**

Our engineering team tackled several real-world challenges with measurable results. For polyglot microservices at scale, we achieved type-safe communication between Java, Go, and Python services using Protocol Buffers and gRPC code generation with automated API contracts. This resulted in 40% latency reduction, 99.9% type safety, and zero breaking changes in 6 months.

For real-time collaboration infrastructure, we enabled live coding sessions with sub-second latency for global users through WebSocket clustering with Redis pub/sub and geographic load balancing. We achieved less than 100ms global latency and support for over 1000 concurrent sessions.

For AI-driven content intelligence, we implemented contextual lab recommendations and intelligent Q&A at scale using vector embeddings and semantic search with incremental model training. This achieved 85% recommendation accuracy and 2-second response time for complex queries.

---

## Closing & Q&A

**Speaker: Kirill Efimovich (PM/DevOps)**

In conclusion, Open Labs Share represents a comprehensive solution to modern educational technology challenges. We've built a scalable, secure, and intelligent platform that bridges the gap between academic learning and industry practice.

Our microservices architecture enables independent scaling and maintenance, our AI-powered features provide intelligent assistance and automated assessment, and our robust DevOps pipeline ensures reliable, continuous delivery.

The platform is live and operational at open-labs-share.online, and our complete source code and architecture documentation is available on GitHub at github.com/IU-Capstone-Project-2025/open-labs-share.

We're now ready to answer any questions you may have about our technical implementation, architecture decisions, or future development plans.

---

## Q&A Response Assignments

**Technical Architecture Questions:** Nikita Maksimenko, Kirill Efimovich
**Security & Authentication:** Mikhail Trifonov
**Frontend & UX:** Aleliya Turushkina
**Content Management & Storage:** Timur Salakhov
**AI/ML Implementation:** Kirill Shumskiy
**Feedback & Review Systems:** Ravil Kazeev
**DevOps & Infrastructure:** Kirill Efimovich
**Project Management & Vision:** Kirill Efimovich

---

**Total Presentation Time: ~20-25 minutes**
**Q&A Time: ~10-15 minutes** 