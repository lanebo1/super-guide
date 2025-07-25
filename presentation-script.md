# Open Labs Share - Presentation Script

**Practicum Project Defense, S25**

**Team:** Kirill Efimovich, Aleliya Turushkina, Mikhail Trifonov, Nikita Maksimenko, Timur Salakhov, Ravil Kazeev, Kirill Shumskiy

---

## Kirill Efimovich - Slide #1 - Title Slide & Opening

Good morning, everyone. I'm Kirill, the project manager and DevOps engineer for our team. Today we're excited to present Open Labs Share - a learning platform that bridges the gap between academic and practice through microservices architecture.

---

## Nikita Maksimenko - Slide #3 - The Problem: Skills Gap in Tech Education

We found that typical learning lacks practice required by all jobs. Our mission is to use our engineering skills to create a platform where theory meets practice.

---

## Kirill Efimovich - Slide #4 - Meet the Team

About us: I've handled project leadership and DevOps engineering, Mikhail Nikita Timur and Ravil worked on backend, Kirill developed ML and Aleliya designed and implemented frontend.

---

## Kirill Efimovich - Slide #5 - Product Vision

So, what is Open Labs Share as a product? It is a content creation system, improved learning experience with structured feedback. With Marimo elements and chat and code autograding powered by ML services we created something that is not just a learning platform, but a learning experience.

---

## Nikita Maksimenko - Slide #6 - Technical Vision

deleted slide

---

## Aleliya Turushkina - Slide #7 - Live Technical Demo

_Now I'll demonstrate our platform's core capabilities. First, you'll see our secure authentication system with OAuth2 and JWT implementation. Next, I'll show our intelligent lab discovery feature powered by ML recommendations and advanced search capabilities. Then we'll explore our advanced development workflow with real-time collaboration and submission pipeline. I'll demonstrate our intelligent review engine with AI-assisted peer matching and quality scoring. Finally, we'll look at our analytics dashboard providing real-time metrics and performance insights._

[Conduct live demo showing each feature]

---

## Nikita Maksimenko - Slide #8 - Advanced System Architecture

Before proceeding with each service, take a look at this monster. On the picture you can see architecture of the whole system. We have 10 microservices, 9 separate databases and two main protocols of communicaiton, dark blue arrows are gRPC, purple ones - HTTP REST API. We use PostgreSQL databases for metadata storage. MongoDB for large texts as comments or reviews. MinIO for all files and assets used in your system. This enshures scalable, highload and foult-tolerance architecture. Now, let's dive into each service.

---


---

## Aleliya Turushkina - Slide #11 - Frontend: Tech Stack & Connections

Technically, the frontend uses React with Vite for fast build. We use specialized libraries like Markdown and KaTeX for content rendering.

---

## Mikhail Trifonov - Slide #13 - Authentication Service (Title)

Let's start with our Authentication Service, which is the foundation of our security architecture, ensuring every user interaction is protected.

---

## Mikhail Trifonov - Slide #14 - Authentication Service: Primary Use Case

This service manages user authentication through sign-in and sign-up with gRPC calls to the Users Service, generating JWT access and refresh tokens to control user sessions. It also serves as a security gateway validating all API requests for protected resources.

---

## Mikhail Trifonov - Slide #15 - Authentication Service: Tech Stack & Connections

Auth Service uses Java with Spring Boot for REST API, Spring Security with JWT for token management. We use gRPC for high-performance calls to the Users Service and token validation for the API Gateway.

---

## Mikhail Trifonov - Slide #16 - Authentication Service: Problems & Solutions

We solved several problems, one of them was in access tokens remaining valid after user logout, which we addressed through token blacklisting and invalidation.

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

The main challenge was in the create-drop ORM strategy causing inconsistency during container restarts, which was solved by using Flyway.

---

## Nikita Maksimenko - Slide #21 - API Gateway (Title)

The API Gateway acs as a central coordinator in the system communicating with 6 microservices. 

---

## Nikita Maksimenko - Slide #22 - API Gateway: Primary Use Case


API Gateway checks users authentication, validates all data before forwarding it to the backend services. Most requsts require buisness logic execution with data from several services. 


---

## Nikita Maksimenko - Slide #23 - API Gateway: Tech Stack & Connections

We use the same java tech stack.


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

While we developed this service, we met several problems, but the main is connected to SQL queries. Some people may love writing direct SQL queries, but it's not flexible: each purpose - separate query, separate function to call... That's why we used ORM to make it simple, clean, and flexible to develop a service

---

## Timur Salakhov - Slide #29 - Labs Service (Title)

Then goes Labs Service. Its purpose is approximately the same: to handle Labs management

---

## Timur Salakhov - Slide #30 - Labs Service: Primary Use Case

It deals with labs, submissions, and assets management. Stores all metadata and provides searching functionality, including tag and grading system

---

## Timur Salakhov - Slide #31 - Labs Service: Tech Stack & Connections

Stack is pretty much the same as Articles Service: Python and gRPC as well. However, integrations little differs: there are API Gateway, PostgreSQL and MinIO, but there also a MongoDB database ->

---

## Timur Salakhov - Slide #32 - Labs Service: Problems & Solutions

-> which we used to store lab submissions descriptions. We could store everything in PostgreSQL but we found out MongoDB is useful in terms of big texts, so thats why we used it

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

The main challenge was in design. High load on one service managing metadata, connections with other services, and execution simultaneously was resolved through dual-service architecture separating management from execution.

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

We resolved three critical problems: university network NAT blocked external access to our self-hosted server, solved by using CloudPub to create a tunnel for public access. Risk of downtime during deployment, is fixed by implementing a Blue-Green strategy.

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
