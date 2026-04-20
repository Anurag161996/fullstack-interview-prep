# Java Interview Prep - Senior Backend

A comprehensive interview preparation resource with 1165+ questions across 28 topics.

## File Structure

```
├── index.html          # Main HTML page
├── styles.css          # All CSS styling
├── app.js              # Application logic
├── ai.js               # AI/ML questions
└── data/               # Topic data files (28 files)
    ├── java.js
    ├── spring.js
    ├── hibernate.js
    ├── threads.js
    ├── sql.js
    ├── rest.js
    ├── redis.js
    ├── kafka.js
    ├── hld.js
    ├── microservices.js
    ├── docker.js
    ├── kubernetes.js
    ├── aws.js
    ├── testing.js
    ├── patterns.js
    ├── solid.js
    ├── maven.js
    ├── dsa.js
    ├── javascript.js
    ├── react.js
    ├── nextjs.js
    ├── grpc.js
    ├── reactive.js
    ├── security.js
    ├── observability.js
    ├── performance.js
    ├── cicd.js
    └── ai.js
```

## Topics Covered

| Topic | Questions |
|---|---|
| **Core Java** (☕) - OOP, JVM, Collections, Streams, Java 17/21 | 93 |
| **Spring Boot** (🌿) - DI, REST, configuration, profiles | 47 |
| **Hibernate & JPA** (🗄) - ORM, caching, transactions | 32 |
| **Multithreading** (⚡) - Concurrency, executors, synchronization | 30 |
| **SQL & Databases** (🏛) - Queries, indexing, transactions | 38 |
| **REST APIs** (🔗) - Design principles, versioning | 30 |
| **Redis & Caching** (🔴) - Caching strategies, data structures | 15 |
| **Apache Kafka** (📨) - Messaging, streaming, consumer groups | 19 |
| **HLD & System Design** (🏗) - Architecture, scalability | 36 |
| **Microservices** (☁) - Patterns, Spring Cloud, resilience | 15 |
| **Docker** (🐳) - Containerization, multi-stage builds | 23 |
| **Kubernetes** (⚙) - Orchestration, deployments, services | 25 |
| **AWS** (☁) - EC2, S3, RDS, Lambda, ECS | 25 |
| **Testing** (🧪) - Unit, integration, E2E testing | 24 |
| **Design Patterns** (🧩) - Creational, structural, behavioral | 24 |
| **SOLID Principles** (🔩) - OOP design principles | 12 |
| **Maven** (🔧) - Build tools, dependency management | 11 |
| **DSA** (📊) - Data structures & algorithms for backend | 23 |
| **JavaScript** (🟨) - ES6+, async, closures, event loop | 245 |
| **React** (⚛) - Hooks, state management, performance | 147 |
| **Next.js** (▲) - SSR, SSG, routing, API routes | 104 |
| **gRPC** (🔌) - Protocol Buffers, streaming, service design | 22 |
| **Reactive Programming** (🔄) - Project Reactor, RxJava | 22 |
| **Security** (🔐) - Auth, OAuth2, JWT, OWASP | 29 |
| **Observability** (📡) - Logging, metrics, tracing | 17 |
| **Performance** (🚀) - Profiling, optimization, tuning | 12 |
| **CI/CD** (🔁) - Pipelines, GitHub Actions, deployment | 24 |
| **AI/ML** (🤖) - LLMs, embeddings, RAG, AI integration | 21 |

## Usage

Simply open `index.html` in a web browser. No build step or server required.

For local development with hot reload:
```bash
python3 -m http.server 8000
# Visit http://localhost:8000
```

## Features

- 🔍 Search across all topics and questions
- 🎯 Filter by category (Java Core, Spring, Data & DB, Frontend, etc.)
- 📊 Difficulty levels (Easy, Medium, Hard)
- 💡 Detailed answers with code examples
- 📱 Fully responsive design
- 🌙 Dark/Light theme support
- 🔖 Bookmark questions for later review

## Adding New Questions

To add questions to a topic, edit the corresponding file in `data/`:

```javascript
// In data/java.js
SEC_JAVA.qs.push(
  {q:"Your question here?", d:"easy",
   a:"Your detailed answer with <strong>HTML</strong> and <code>code</code>."}
);
```

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge).
