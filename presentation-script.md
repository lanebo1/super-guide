# Open Labs Share - Presentation Script

**Practicum Project Defense, S25**

**Team:** Kirill Efimovich, Aleliya Turushkina, Mikhail Trifonov, Nikita Maksimenko, Timur Salakhov, Ravil Kazeev, Kirill Shumskiy

---

## Kirill Efimovich - Slide #1 - Title Slide & Opening

Good morning, everyone. I'm Kirill, the project manager and DevOps engineer for our team. Today we're excited to present Open Labs Share - a learning platform that bridges the gap between academic and practice through microservices architecture.

---

## Kirill Efimovich - Slide #2 - Agenda

About agenda. We'll start with the problem and our solve, introduce our team, and show demo. Then we'll dive into frontend engineering, explore our system architecture aligned with backend microservices, discuss our ML integration, cover our DevOps things, and then wrap it up for discussion.

---

## Kirill Efimovich - Slide #3 - The Problem: Skills Gap in Tech Education

We identified key challenges in education technology: limited real-world project experience, inefficient mentor-learner matching, and poor feedback loops between industry and education. Our engineering mission is to build a platform that connects  experts with young developers through hands-on technical projects.

---

## Kirill Efimovich - Slide #4 - Meet the Team

About us: I've handled project leadership and DevOps engineering, Mikhail managing authentication systems, Nikita designed and implemented API systems, Timur made content systems, Ravil worked on feedback systems, Kirill developed ML and tackeld backend, and Aleliya design.

---

## Kirill Efimovich - Slide #5 - Product Vision

So, what is Open Labs Share? It is a modern learning platform that bridges the gap between academia and practice. We made it: content creation with a version-controlled lab management system enabling experts to publish and maintain high-quality learning materials, guided learning experience with structured submission and review processes that provide meaningful feedback and track progress, smart community building with AI-enhanced assistance for better feedback and user experience, and Marimo elements providing interactive Python notebook execution with widgets for better user experience.

---

## Kirill Efimovich - Slide #6 - Technical Vision

From a technical perspective, Open Labs Share is a microservices-driven learning ecosystem with AI-powered assistance. We have separate services for labs, articles, feedback and more, connected through fast and reliable gRPC inter-service communication, all powered by ML services that provide ML-powered feedback and chat capabilities.

---

## Aleliya Turushkina - Slide #7 - Live Technical Demo

*Now I'll demonstrate our platform's core capabilities. First, you'll see our secure authentication system with OAuth2 and JWT implementation. Next, I'll show our intelligent lab discovery feature powered by ML recommendations and advanced search capabilities. Then we'll explore our advanced development workflow with real-time collaboration and submission pipeline. I'll demonstrate our intelligent review engine with AI-assisted peer matching and quality scoring. Finally, we'll look at our analytics dashboard providing real-time metrics and performance insights.*

[Conduct live demo showing each feature]

---

## Aleliya Turushkina - Slide #8 - Frontend Architecture (Title)

*Our frontend serves as a modern web app that lets users explore and review labs and articles through an interactive, user-friendly interface, bridging the gap between complex backend systems and user-friendly experience. The user interface is built with React and modern web technologies, providing an intuitive experience for both learners and educators.*

---

## Aleliya Turushkina - Slide #9 - Frontend: Main User Interface

*The frontend handles user authentication, profile management, and navigation. It enables users to browse, upload, and review labs and articles, participate in peer review and feedback systems, and interact with real-time features like chat and notifications. Users can seamlessly browse content, submit assignments, participate in peer reviews, and engage in real-time collaboration.*

---

## Aleliya Turushkina - Slide #10 - Frontend: Tech Stack & Connections

*We built this using React, Vite, Tailwind CSS, and React Router for the core framework. Component libraries include React PDF Viewer and Markdown with KaTeX support. For API integration, the frontend communicates with our backend via REST API through the API Gateway, integrating with Auth, Labs, Articles, Submissions, Feedback, and ML services, plus real-time file download support from MinIO.*

---

## Aleliya Turushkina - Slide #11 - Frontend: Problems & Solutions

*We solved two key challenges: first, the lack of viewing capabilities for user submissions and feedback, which we addressed by implementing direct file downloads from MinIO. Second, the inability to view Markdown content using a dark theme, which we solved by implementing comprehensive theme switching and styling across the entire platform.*

---

## Nikita Maksimenko - Slide #12 - Advanced System Architecture

*Before diving into individual services, let me explain our overall system architecture. We've designed an architecture for high availability and horizontal scaling. Our microservices communicate via gRPC for high-performance, type-safe interactions, while the frontend communicates through REST APIs via our centralized API Gateway. This architecture enables us to scale individual components independently, maintain strong service boundaries, and ensure reliable communication between polyglot services written in Java, Go, and Python.*

---

## Mikhail Trifonov - Slide #13 - Authentication Service (Title)

*I'll start with our Authentication Service, which provides stateless JWT-based authentication for enterprise-grade security across the entire Open Labs Share ecosystem. This service is the foundation of our security architecture, ensuring every user interaction is protected while maintaining seamless user experience.*

---

## Mikhail Trifonov - Slide #14 - Authentication Service: Primary Use Case

*This service handles all authentication flows and token lifecycle management for secure access control. It manages user authentication through sign-in and sign-up with gRPC calls to the Users Service. The service generates JWT access and refresh tokens with user claims, verifies signatures, expiration, and blacklist status. It provides session management with logout and token blacklisting for security, and serves as a security gateway validating all API requests for protected resources.*

---

## Mikhail Trifonov - Slide #15 - Authentication Service: Tech Stack & Connections

*Our tech stack uses Java 21 with Spring Boot 3.5 for REST controllers, Spring Security with JWT for token generation, signing, validation, and refresh token support. We use gRPC for high-performance calls to the Users Service and token validation for the API Gateway. An in-memory blacklist stores invalidated tokens for logout functionality, and we provide OpenAPI documentation for interactive API testing.*

---

## Mikhail Trifonov - Slide #16 - Authentication Service: Problems & Solutions

*We solved three critical problems: first, JWT tokens remaining valid after user logout, which we addressed through token blacklisting and invalidation. Second, user data consistency between Auth and Users Services, solved by establishing a single source of truth in the Users Service while the Auth Service fetches data on-demand without storing user information. Third, username changes invalidating current JWTs, resolved through token reissue logic that preserves user sessions seamlessly.*

---

## Mikhail Trifonov - Slide #17 - Users Service (Title)

*The Users Service serves as the single source of truth for all user data with comprehensive profile management and a points system. Every great platform needs a reliable foundation for user data, and I designed this service to be the single source of truth that all other services can trust.*

---

## Mikhail Trifonov - Slide #18 - Users Service: Primary Use Case

*It manages all user data, credentials, and points for solving and reviewing labs. The service handles user registration creating new accounts, credential management storing bcrypt-hashed passwords and validating usernames, emails, and passwords. It provides CRUD operations for user profiles, tracks labs solved and reviewed counts with points balance, and maintains data integrity as the single source of truth for all user-related information.*

---

## Mikhail Trifonov - Slide #19 - Users Service: Tech Stack & Connections

*We use Java 21 with Spring Boot 3.5 for REST controllers and JPA repositories. PostgreSQL stores user data, credentials, points, and lab statistics. Flyway handles database schema versioning and migration management. Our gRPC server provides APIs for user validation, data retrieval, and points updates to other microservices.*

---

## Mikhail Trifonov - Slide #20 - Users Service: Problems & Solutions

*Two main challenges were resolved: first, the create-drop ORM strategy causing inconsistency during container restarts, solved by implementing Flyway for SQL table creation instead of auto-creation with a validate strategy. Second, strict control requirements for the points system due to its monetary purpose, addressed through transactional methods preventing inconsistency in balance and counters.*

---

## Nikita Maksimenko - Slide #21 - API Gateway (Title)

*The API Gateway serves as the centralized entry point coordinating frontend REST API requests, executing business logic, and routing them to backend microservices via gRPC. The API Gateway is the conductor of our microservices orchestra, ensuring all services work in harmony while providing a clean, unified interface to the frontend.*

---

## Nikita Maksimenko - Slide #22 - API Gateway: Primary Use Case

*It provides centralized entry point serving as the unified access layer for all client REST API requests. The gateway handles request routing directing incoming requests to appropriate microservices including auth, user, article, and lab services via gRPC. It manages authentication and security validating JWT tokens and user permissions. The service handles cross-cutting concerns like logging, request tracing, and error handling for all API traffic, plus business logic execution aggregating data and enforcing business rules beyond simple routing.*

---

## Nikita Maksimenko - Slide #23 - API Gateway: Tech Stack & Connections

*Our tech stack uses Java Spring Boot with REST-to-gRPC translation. We receive data from frontend via REST as the simplest and most widely supported web communication method. Our security layer intercepts incoming REST requests for authentication and authorization ensuring secure access and centralized permission checks. The gRPC client routes requests internally to backend microservices providing high-speed, type-safe, and scalable service-to-service communication. Response handling returns responses to clients through the gateway centralizing response handling and error management.*

---

## Nikita Maksimenko - Slide #24 - API Gateway: Problems & Solutions

*We addressed three problems: too many services and people to communicate with, solved by creating clear communication rules and defining issue execution order for efficient collaboration. Unclear models from both frontend and backend, resolved by establishing detailed requirements for each request step ensuring consistency and clarity. Lack of data checks on frontend, addressed using Jackson validators in request models to enforce data integrity before processing.*

---

## Timur Salakhov - Slide #25 - Articles Service (Title)

*The Articles Service serves as the central repository for all scientific articles and research papers, enabling authors to publish content and students to access educational materials. Knowledge should be accessible and well-organized, and I built this service to be the backbone of our content ecosystem, where every article finds its perfect place.*

---

## Timur Salakhov - Slide #26 - Articles Service: Primary Use Case

*This service manages all articles and assets metadata. It provides CRUD operations for article details, handles article assets in an independent storage system, organizes and updates metadata for articles and assets, and provides article searching based on title and abstract.*

---

## Timur Salakhov - Slide #27 - Articles Service: Tech Stack & Connections

*We built this using Python 3.12 as our programming language with gRPC for inter-service communication. The service integrations include the API Gateway receiving and returning data in gRPC format, PostgreSQL database storing all articles and asset metadata, and MinIO storage system storing all article assets.*

---

## Timur Salakhov - Slide #28 - Articles Service: Problems & Solutions

*We resolved four key challenges: difficult database interaction via SQL queries, solved by using SQLAlchemy ORM for convenient and flexible database interaction. The need to organize article files systematically, addressed by creating structured MinIO bucket organization with articles organized by article ID. Large files causing timeout issues during upload, resolved by implementing streaming gRPC uploads for efficient file transfer. Frontend searching across articles, solved by moving search functionality to the service and building text search with pagination.*

---

## Timur Salakhov - Slide #29 - Labs Service (Title)

*The Labs Service serves as the central repository for all laboratory work and student submissions, enabling teachers to create assignments and students to submit solutions with comprehensive grading and feedback. Labs are where theory meets practice, and I created this service to handle the complexity of assignments and submissions while keeping the learning process smooth and engaging.*

---

## Timur Salakhov - Slide #30 - Labs Service: Primary Use Case

*This service manages all labs, submissions, and educational content. It provides CRUD operations for lab assignments with tags, handles submissions with text content and file assets, organizes labs with flexible tagging and search capabilities, and tracks submission status and grade workflow.*

---

## Timur Salakhov - Slide #31 - Labs Service: Tech Stack & Connections

*We use Python 3.12 with hybrid database architecture and MinIO storage. Service integrations include the API Gateway as single entry point for all requests, PostgreSQL database storing labs, submissions, tags, and asset metadata, MongoDB database storing submission text content for flexible storage, and MinIO storage system storing lab and submission assets in organized buckets.*

---

## Timur Salakhov - Slide #32 - Labs Service: Problems & Solutions

*We addressed three main problems: complex data relationships between labs, submissions, and tags, solved using SQLAlchemy models with proper foreign keys and many-to-many relationships for structured data management. Large submission text content causing database bloat, resolved by implementing hybrid storage with metadata in PostgreSQL and text content in MongoDB for flexibility. The need to organize files systematically, addressed by creating structured MinIO bucket organization for labs and submissions.*

---

## Ravil Kazeev - Slide #33 - Feedback Service (Title)

*The Feedback Service centralizes feedback and discussion by managing detailed lab reviews, supporting file attachments, and powering threaded conversations for both labs and articles. Great learning happens through meaningful feedback, and I designed this service to foster rich discussions and provide constructive guidance that helps students grow.*

---

## Ravil Kazeev - Slide #34 - Feedback Service: Primary Use Case

*This comprehensive feedback and discussion management system enables reviewers to create, update, and delete detailed feedback on submissions using Markdown for text and code formatting. It powers a threaded commenting system for both labs and articles with nested replies keeping conversations structured and easy to follow. The service allows multiple file attachments per feedback entry, using efficient gRPC streaming to handle large uploads and downloads without high memory usage.*

---

## Ravil Kazeev - Slide #35 - Feedback Service: Tech Stack & Connections

*We built this using Go 1.24 as a high-performance, concurrent service ideal for I/O-heavy tasks. Our gRPC server provides a typed API for feedback, comments, and file streaming. We implemented a multi-storage backend with PostgreSQL storing structured feedback metadata, MongoDB storing unstructured comments and feedback content, and MinIO providing object storage for all file attachments.*

---

## Ravil Kazeev - Slide #36 - Feedback Service: Problems & Solutions

*Three major problems were resolved: first, a single database was inefficient for managing varied data types including metadata, text, and files. We implemented a multi-storage architecture using the best database for each job. Second, uploading large files as a single request was unreliable, leading to timeouts and memory errors. We re-architected attachment handling using gRPC streaming, processing files in small chunks for efficient and robust transfers. Third, file downloads through the Feedback service would create a bottleneck. We configured the MinIO bucket for public read access, allowing the service to provide direct file URLs to the frontend and offload all download traffic.*

---

## Mikhail Trifonov - Slide #37 - Marimo Service (Title)

*The Marimo Service is a dual-architecture microservice providing real-time interactive Python notebook execution powered by the Marimo library. Interactive coding should be accessible to everyone, and I built this service to bring the power of Jupyter-like notebooks directly into our platform with seamless execution.*

---

## Mikhail Trifonov - Slide #38 - Marimo Service: Primary Use Case

*This service enables interactive code execution and data visualization through cells with Python code. It provides notebook management with CRUD operations for marimo components linked to labs and articles. Session orchestration starts and stops interactive Python sessions with TTL. Code execution happens in real-time with output capture and error handling. Asset management handles upload and download of datasets and files for notebook use. Interactive widgets provide basic Marimo input widgets whose values can be used in code, and cross-cell state memory ensures variables and modules from executed cells are available in other cells.*

---

## Mikhail Trifonov - Slide #39 - Marimo Service: Tech Stack & Connections

*Our tech stack uses Java for metadata management with Python native code execution. The Java Manager handles REST API and metadata while Python executes notebooks. PostgreSQL tracks notebook metadata, user sessions, and execution trails with TTL cleanup. MinIO provides object storage for notebook files and user-uploaded assets. gRPC enables communication between Java Manager and Python Executor for execute requests and session management, with Marimo providing interactive notebook execution with custom widgets.*

---

## Mikhail Trifonov - Slide #40 - Marimo Service: Problems & Solutions

*We solved three challenges: high load on one service managing metadata, connections with other services, and execution simultaneously, resolved through dual-service architecture separating management from execution. Managing variables and modules across multiple code cells, solved using sessions for notebooks to track existing and erased variables and modules. Marimo widgets incompatibility with our needs and technology, addressed by creating custom design widgets based on Marimo widgets with configurable behavior fully under our control.*

---

## Kirill Shumskiy - Slide #41 - ML Service (Title)

*The ML Service provides advanced AI-powered features with intelligent assistance and automated grading capabilities for enhanced learning experience. AI should empower learning, not replace human connection, and I developed these intelligent features to provide personalized assistance while preserving the human element in education.*

---

## Kirill Shumskiy - Slide #42 - ML Service: Primary Use Case

*We deliver two powerful AI enhancements for the learning platform. First, our AI RAG Assistant provides context-aware code and documentation help, leveraging Retrieval-Augmented Generation to deliver accurate, real-time support to students. Second, our Autograding system offers automated code assessment for evaluating submissions instantly, ideal for learning platforms.*

---

## Kirill Shumskiy - Slide #43 - ML Service: Tech Stack & Connections

*Our FastAPI backend uses specialized AI models and infrastructure. For the AI RAG Assistant, we use Qwen2.5-Coder-1.5B-Instruct for local inference, Qdrant vector store, and BAAI/bge-small-en-v1.5 embeddings. For Autograding, we use deepseek-r1-distill-llama-70b for groq inference and Menagerie dataset for graded CS1 assignments evaluation. Our core architecture includes FastAPI-based backend with three-layer structure, Celery for asynchronous tasks, and Redis for caching and message broker.*

---

## Kirill Shumskiy - Slide #44 - ML Service: Infrastructure

*Our ML pipeline and deployment architecture includes recursive chunking for long documents, embedding via transformer model BGE, Vector DB with Qdrant, relevance thresholding using cosine similarity, and RAG with prompt templating for generation. This creates a comprehensive AI system that can understand context and provide intelligent responses to user queries.*

---

## Kirill Efimovich - Slide #45 - DevOps & Infrastructure (Title)

Our DevOps infrastructure represents a journey from manual processes to a fully automated pipeline. We engineered a robust DevOps foundation to enable rapid development, consistent testing, and reliable, zero-downtime deployments for our platform. Reliable infrastructure is invisible when it works perfectly, and I built our DevOps pipeline to be so robust and automated that developers can focus on innovation, not deployment worries.

---

## Kirill Efimovich - Slide #46 - DevOps: Primary Use Case

Our automated deployment pipeline and infrastructure management accelerates delivery by fully automating the build, test, and deployment lifecycle. We ensure stability by creating reproducible environments with Docker for development and production. We also provide team help tools to automate issues managing and PR notifiers to keep the team perfectly synchronized.

---

## Kirill Efimovich - Slide #47 - DevOps: Tech Stack & Connections

Key GitHub Actions workflows include compilation validation ensuring all services compile, test execution running unit and integration tests, Docker build validation that builds, validates and pushes images to GHCR, and deployment automation that handles the Blue-Green deployment logic.

---

## Kirill Efimovich - Slide #48 - DevOps: Infrastructure

Our infrastructure uses a Green-Blue strategy providing zero downtime with seamless updates. The workflow deploys new versions Green alongside Production Blue, tests Green environment internally, switches HAProxy to route traffic to Green, and keeps Blue for instant rollback. Our server and networking setup includes a self-managed server on Ubuntu 24.04 with 6-Core CPU, 16GB RAM, and 240GB SSD. We use NGINX and HAProxy for proxying, CloudPub for public NAT traversal, and cAdvisor for container metrics.

---

## Kirill Efimovich - Slide #49 - DevOps: Problems & Solutions

We resolved three critical problems: university network NAT blocking external access to our self-hosted server, solved by using CloudPub to create a secure tunnel for public access after issues with Cloudflare. The initial CI/CD pipeline being complex and requiring many iterations to stabilize, resolved through persistent, collaborative effort developing reliable, modular GitHub Actions workflows. Risk of downtime during manual deployments, addressed by fully automating the deployment process and implementing a Blue-Green strategy ensuring zero-downtime updates.

---

## Kirill Efimovich - Slide #50 - Thank You & Q&A

In conclusion, Open Labs Share represents a comprehensive solution to modern educational technology challenges. We've built a scalable, secure, and intelligent platform that bridges the gap between academic learning and industry practice. Our microservices architecture enables independent scaling and maintenance, our AI-powered features provide intelligent assistance and automated assessment, and our robust DevOps pipeline ensures reliable, continuous delivery. The platform is live and operational at open-labs-share.online. We're now ready to answer any questions you may have about our technical implementation, architecture decisions, or future development plans.

---

## Q&A Response Assignments

**Technical Architecture Questions:** Nikita Maksimenko, Mikhail Trifonov, Kirill Efimovich
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