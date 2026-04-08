# Java Interview Prep - Senior Backend

A comprehensive interview preparation resource with 437+ questions across 18 topics.

## File Structure

```
Interview/
├── index.html          # Main HTML page
├── styles.css          # All CSS styling
├── app.js             # Application logic
├── data/              # Topic data files (17 files)
│   ├── java.js
│   ├── spring.js
│   ├── hibernate.js
│   ├── threads.js
│   ├── sql.js
│   ├── rest.js
│   ├── redis.js
│   ├── kafka.js
│   ├── hld.js
│   ├── microservices.js
│   ├── docker.js
│   ├── aws.js
│   ├── testing.js
│   ├── patterns.js
│   ├── solid.js
│   ├── maven.js
│   └── dsa.js
└── data.js.backup     # Original monolithic data file
```

## Topics Covered

1. **Core Java** (☕) - OOP, JVM, Collections, Streams, Java 17/21
2. **Spring Boot** (🌿) - DI, REST, configuration, profiles
3. **Hibernate & JPA** (🗄) - ORM, caching, transactions
4. **Multithreading** (⚡) - Concurrency, executors, synchronization
5. **SQL & Databases** (🏛) - Queries, indexing, transactions
6. **REST APIs** (🔗) - Design principles, versioning
7. **Redis & Caching** (🔴) - Caching strategies, data structures
8. **Apache Kafka** (📨) - Messaging, streaming, consumer groups
9. **HLD & System Design** (🏗) - Architecture, scalability
10. **Microservices** (☁) - Patterns, Spring Cloud, resilience
11. **Docker** (🐳) - Containerization, multi-stage builds
12. **AWS** (☁) - EC2, S3, RDS, Lambda, ECS
13. **Testing** (🧪) - Unit, integration, E2E testing
14. **Design Patterns** (🧩) - Creational, structural, behavioral
15. **SOLID Principles** (🔩) - OOP design principles
16. **Maven** (🔧) - Build tools, dependency management
17. **DSA** (📊) - Data structures & algorithms for backend

## Usage

Simply open `index.html` in a web browser. No build step or server required.

For local development with hot reload:
```bash
python3 -m http.server 8000
# Visit http://localhost:8000
```

## Features

- 🔍 Search across all topics and questions
- 🎯 Filter by category (Java Core, Spring, Data & DB, etc.)
- 📊 Difficulty levels (Easy, Medium, Hard)
- 💡 Detailed answers with code examples
- 📱 Fully responsive design
- 🌙 Dark theme optimized for readability

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
