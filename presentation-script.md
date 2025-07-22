# Open Labs Share - Presentation Script

**Practicum Project Defense, S25**

**Team:** Kirill Efimovich, Aleliya Turushkina, Mikhail Trifonov, Nikita Maksimenko, Timur Salakhov, Ravil Kazeev, Kirill Shumskiy

---

## Kirill Efimovich - Slide #1 - Title Slide & Opening

Good morning, everyone. I'm Kirill, the project manager and DevOps engineer for our team. Today we're excited to present Open Labs Share - a learning platform that bridges the gap between academic and practice through microservices architecture.

---

## Kirill Efimovich - Slide #2 - Agenda

About agenda. We'll start with the problem and our solve, introduce our team, and show demo. Then we'll dive into tech stuff, and then wrap it up for discussion.

---

## Kirill Efimovich - Slide #3 - The Problem: Skills Gap in Tech Education

We identified key challenges in education technology, the main is inefficient mentor-learner matching, and poor feedback loops. Our engineering mission is to build a platform that connects experts with young developers through practical projects.

---

## Kirill Efimovich - Slide #4 - Meet the Team

About us: I've handled project leadership and DevOps engineering, Mikhail managing authentication systems, Nikita designed and implemented API systems, Timur made content systems, Ravil worked on feedback systems, Kirill developed ML and tackeld backend, and Aleliya designed and implemented frontend.

---

## Kirill Efimovich - Slide #5 - Product Vision

So, what is Open Labs Share as a product? it is a content creation for high-quality learning materials, improved learning experience with structured review processes. With Marimo elements and chat and code autograding powered by ML services we created something that is not just a learning platform, but a learning experience.

---

## Kirill Efimovich - Slide #6 - Technical Vision

From a technical perspective, Open Labs Share is a microservices ecosystem with ML additions. We have separate services for... everything, connected through fast and reliable gRPC. Included Marimo elements and chat and code autograding ML services are also part of the ecosystem.

---

## Aleliya Turushkina - Slide #7 - Live Technical Demo

_Now I'll demonstrate our platform's core capabilities. First, you'll see our secure authentication system with OAuth2 and JWT implementation. Next, I'll show our intelligent lab discovery feature powered by ML recommendations and advanced search capabilities. Then we'll explore our advanced development workflow with real-time collaboration and submission pipeline. I'll demonstrate our intelligent review engine with AI-assisted peer matching and quality scoring. Finally, we'll look at our analytics dashboard providing real-time metrics and performance insights._

[Conduct live demo showing each feature]

---

## Aleliya Turushkina - Slide #8 - Frontend Architecture (Title)

The frontend is a modern web app offering an intuitive, interactive experience with labs and articles. It serves as the main gateway, ensuring smooth navigation and interaction with core features.

---

## Aleliya Turushkina - Slide #9 - Frontend: Main User Interface

The frontend handles critical functionalities such as user authentication, profile management, and dynamic navigation. It allows users to browse, upload, and review labs and articles, participate in peer review processes, and communicate with real-time features like comments.

---

## Aleliya Turushkina - Slide #10 - Frontend: Tech Stack & Connections

Technically, the frontend uses React with Vite for fast builds, Tailwind CSS for responsive styling, and React Router for SPA navigation. For backend communication, the frontend integrates with REST APIs via an API Gateway, plus real-time file download support from MinIO.

---

## Aleliya Turushkina - Slide #11 - Frontend: Problems & Solutions

We have the problem of the inability to view Markdown content using a dark theme, which we solved by implementing comprehensive theme switching and styling across the entire platform.

---

## Nikita Maksimenko - Slide #12 - Advanced System Architecture

Before proceeding with each service, take a look at this monster. This is a complete architecture of our project. We use best microservice practices to make a scalable and high-performance application. 

---

## Mikhail Trifonov - Slide #13 - Authentication Service (Title)

I'll start with our Authentication Service, which is the foundation of our security architecture, ensuring every user interaction is protected.

---

## Mikhail Trifonov - Slide #14 - Authentication Service: Primary Use Case

This service manages user authentication through sign-in and sign-up with gRPC calls to the Users Service, generating JWT access and refresh tokens to control user sessions. It also serves as a security gateway validating all API requests for protected resources.

---

## Mikhail Trifonov - Slide #15 - Authentication Service: Tech Stack & Connections

Auth Service uses Java with Spring Boot for REST API, Spring Security with JWT for token management. We use gRPC for high-performance calls to the Users Service and token validation for the API Gateway.

---

## Mikhail Trifonov - Slide #16 - Authentication Service: Problems & Solutions

We solved three critical problems: first, access tokens remaining valid after user logout, which we addressed through token blacklisting and invalidation. Second, user data consistency between Auth and Users Services, solved by transferring the storage of all user data to the Users Service. Third, username changes invalidating current access tokens, resolved through token reissue logic that preserves user sessions seamlessly.

---

## Mikhail Trifonov - Slide #17 - Users Service (Title)

The Users Service serves as the single source of truth for all user data and a points system management.

---

## Mikhail Trifonov - Slide #18 - Users Service: Primary Use Case

It provides CRUD operations for user profiles, tracks labs solved and reviewed counts with points balance, and maintains data integrity as the single source of truth for all user-related information.

---

## Mikhail Trifonov - Slide #19 - Users Service: Tech Stack & Connections

We use same framework as for Auth Service. PostgreSQL stores user data and points. Flyway handles database migration management and gRPC server provides API for data retrieval and updates.

---

## Mikhail Trifonov - Slide #20 - Users Service: Problems & Solutions

Two main challenges were resolved: first, the create-drop ORM strategy causing inconsistency during container restarts, solved by using Flyway. Second, strict control for the points system was needed, addressed through transactional methods preventing any counters inconsistency.

---

## Nikita Maksimenko - Slide #21 - API Gateway (Title)

The API Gateway centrally coordinates frontend REST API requests, executes business logic, and routes them to backend microservices via gRPC

---

## Nikita Maksimenko - Slide #22 - API Gateway: Primary Use Case

The API Gateway handles REST requests, validates user authentication, executes platform business logic that requires multiple services communication via gRPC. 

---

## Nikita Maksimenko - Slide #23 - API Gateway: Tech Stack & Connections

We use REST for external API for it's simplicity. gRPC enhances speed of content delivery between microservices. Jakarta Validation and Lombok libraries reduce boilerplate code and enhances service security. Core tech is Java 21 and Spring Framework.

---

## Nikita Maksimenko - Slide #24 - API Gateway: Problems & Solutions

About problems. We had to fix communication problems in team by introducing strict rules. To ensure fault tolerance of backend system we must have implemented checks by ourselfs.

---

## Timur Salakhov - Slide #25 - Articles Service (Title)

After we handled user management and created the basis for the rest of the microservices, we needed to create a service for Articles management - the Article Service.

---

## Timur Salakhov - Slide #26 - Articles Service: Primary Use Case

It deals with articles and its assets management. Stores all metadata and provides searching functionality

---

## Timur Salakhov - Slide #27 - Articles Service: Tech Stack & Connections

Articles Service built with Python programming language and exchanges with data via gRPC. It is integrated with API gateway, from which gets all articles requests, and databases: PostgreSQL for metadata storage and MinIO for assets storage

---

## Timur Salakhov - Slide #28 - Articles Service: Problems & Solutions

While I developed this service, I met several problems, but the main problem is "Difficult interaction with database via SQL quieries". Some people may love write direct SQL quieries, but it's not flexible in terms of development: for each purpose you need to write SQL quieries, separate function to call... It's difficult. That's why I used SQLAlchemy ORM system to make it simple, clean, and flexible to develop a service

---

## Timur Salakhov - Slide #29 - Labs Service (Title)

Then goes Labs Service. Its purpose is approximately the same: to handle Labs management

---

## Timur Salakhov - Slide #30 - Labs Service: Primary Use Case

It deals with labs, submissions, and assets management. Stores all metadata and provides searching functionality, including tag and grading system

---

## Timur Salakhov - Slide #31 - Labs Service: Tech Stack & Connections

Tech stack is pretty much the same as Articles Service: Python and gRPC as well. Service Integrations little differs: there are API Gateway, PostgreSQL database and MinIO storage, but there also a MongoDB database and it is about the problem solution

---

## Timur Salakhov - Slide #32 - Labs Service: Problems & Solutions

While I developed Labs Service, I met a many problems, but the main is "Large submission text content causing database bloat". Lab submissions could not only have a file asset, but also a long description text. After some reseach, I conducted to move subsmission description to MongoDB because it useful to store big texts

---

## Ravil Kazeev - Slide #33 - Feedback Service (Title)

The Feedback service handles reviews on lab solutions and provide comment section for both labs and articles to discuss the content by users 

---

## Ravil Kazeev - Slide #34 - Feedback Service: Primary Use Case

The service allows reviewers to create, update, and delete detailed feedback on lab submissions, complete with file attachments. It also provides a threaded commenting system to keep discussions organized and easy to follow.

---

## Ravil Kazeev - Slide #35 - Feedback Service: Tech Stack & Connections

We chose Go for its high performance in concurrent, I/O-heavy tasks. The service communicates with the API Gateway via gRPC, providing a strongly-typed API for all operations. For data, we used a multi-storage approach: PostgreSQL for structured metadata, MongoDB for comments, and MinIO for file attachments.

---

## Ravil Kazeev - Slide #36 - Feedback Service: Problems & Solutions

A major challenge was that downloading files through the service created a bottleneck. We solved this by giving the frontend direct read access to MinIO. Our service now simply provides a file link, offloading all download traffic and improving performance.

---

## Mikhail Trifonov - Slide #37 - Marimo Service (Title)

The Marimo Service provides interactive Python notebook execution with the Marimo library widgets.

---

## Mikhail Trifonov - Slide #38 - Marimo Service: Primary Use Case

This service enables interactive code execution and data visualization through cells with Python code linked to labs and articles and cross-cells session storage. Datasets and files can be uploaded for notebook use, and Interactive widgets provide basic Marimo input widgets whose values can be used in code.

---

## Mikhail Trifonov - Slide #39 - Marimo Service: Tech Stack & Connections

Marimo Service consist of two sub-services. The Java Manager handles REST API and metadata while Python executes notebooks. PostgreSQL tracks notebook metadata and user sessions. MinIO provides object storage for notebook files and user-uploaded assets. gRPC is used for Java Manager and Python Executor communications.

---

## Mikhail Trifonov - Slide #40 - Marimo Service: Problems & Solutions

Three main challenges were solved: high load on one service managing metadata, connections with other services, and execution simultaneously, resolved through dual-service architecture separating management from execution. Managing variables and modules across multiple code cells, solved using sessions for notebooks to track existing and erased variables and modules. Marimo widgets incompatibility with our needs and technology, addressed by creating custom design widgets based on Marimo widgets with configurable behavior fully under our control.

---

## Kirill Shumskiy - Slide #41 - ML Service (Title)

_The ML Service provides advanced AI-powered features with intelligent assistance and automated grading capabilities for enhanced learning experience. AI should empower learning, not replace human connection, and I developed these intelligent features to provide personalized assistance while preserving the human element in education._

---

## Kirill Shumskiy - Slide #42 - ML Service: Primary Use Case

_We deliver two powerful AI enhancements for the learning platform. First, our AI RAG Assistant provides context-aware code and documentation help, leveraging Retrieval-Augmented Generation to deliver accurate, real-time support to students. Second, our Autograding system offers automated code assessment for evaluating submissions instantly, ideal for learning platforms._

---

## Kirill Shumskiy - Slide #43 - ML Service: Tech Stack & Connections

_Our FastAPI backend uses specialized AI models and infrastructure. For the AI RAG Assistant, we use Qwen2.5-Coder-1.5B-Instruct for local inference, Qdrant vector store, and BAAI/bge-small-en-v1.5 embeddings. For Autograding, we use deepseek-r1-distill-llama-70b for groq inference and Menagerie dataset for graded CS1 assignments evaluation. Our core architecture includes FastAPI-based backend with three-layer structure, Celery for asynchronous tasks, and Redis for caching and message broker._

---

## Kirill Shumskiy - Slide #44 - ML Service: Infrastructure

_Our ML pipeline and deployment architecture includes recursive chunking for long documents, embedding via transformer model BGE, Vector DB with Qdrant, relevance thresholding using cosine similarity, and RAG with prompt templating for generation. This creates a comprehensive AI system that can understand context and provide intelligent responses to user queries._

---

## Kirill Efimovich - Slide #45 - DevOps & Infrastructure (Title)

Our DevOps infrastructure built as fully automated pipeline. We engineered a robust DevOps foundation to enable rapid development, automated testing, and our beautiflul deployment.

---

## Kirill Efimovich - Slide #46 - DevOps: Primary Use Case

With our automated deployment we ensure stability by creating reproducible environments with Docker for development and production. We also provide team help tools to automate issues managing and PR notifiers to keep the team in sync.

---

## Kirill Efimovich - Slide #47 - DevOps: Tech Stack & Connections

GitHub Actions workflows include services compilation validation, test execution. Also, Docker build validation that builds, validates and pushes images to GHCR as a part of the deployment pipeline, and deployment itslef that handles the Blue-Green deployment logic.

---

## Kirill Efimovich - Slide #48 - DevOps: Infrastructure

Our infrastructure uses a Green-Blue strategy providing zero downtime with seamless updates. Green deploys at server, tests it, and if it healthy then haproxy switches traffic to new version. Blue is kept for instant rollback.

---

## Kirill Efimovich - Slide #49 - DevOps: Problems & Solutions

We resolved three critical problems: university network NAT blocked external access to our self-hosted server, solved by using CloudPub to create a tunnel for public access. The initial CI pipeline was complex -> resolved through teammates feedback and improvements. Risk of downtime during manual deployments, addressed by implementing a Blue-Green strategy ensuring zero-downtime updates.

---

## Kirill Efimovich - Slide #50 - Thank You & Q&A

And, wrapping it up, we're now ready to answer any questions you may have about our technical implementation, architecture decisions, or future development plans.

---

## Q&A Response Assignments

**Technical Architecture Questions:** Nikita Maksimenko, Mikhail Trifonov, Kirill Efimovich \
**Security & Authentication:** Mikhail Trifonov \
**Frontend & UX:** Aleliya Turushkina \
**Content Management & Storage:** Timur Salakhov \
**AI/ML Implementation:** Kirill Shumskiy \
**Feedback & Review Systems:** Ravil Kazeev \
**DevOps & Infrastructure:** Kirill Efimovich \
**Project Management & Vision:** Kirill Efimovich

---

**Total Presentation Time: ~20-25 minutes** \
**Q&A Time: ~10-15 minutes**
