# Tech Stack

## Backend

- **Runtime:** Node.js with TypeScript
- **Framework:** Express.js or Fastify (prefer Fastify for performance)
- **Language:** TypeScript (strict mode enabled)
- **API Style:** REST or GraphQL depending on use case
- **Validation:** Zod for runtime type validation

## Frontend

- **Framework:** React.js with TypeScript
- **Styling:** Tailwind CSS
- **Build Tool:** Vite
- **State Management:** React Query (server state), Zustand (client state)
- **Routing:** React Router v6+

## Database

- **Primary:** PostgreSQL
- **ORM/Query Builder:** Prisma
- **Migrations:** Managed via ORM migration tooling

## Cache

- **Engine:** Redis
- **Use Cases:** Session storage, API response caching, rate limiting, pub/sub

## Application Architecture

- **Style:** Modern containerized or serverless
- **Container:** Docker + ECS Fargate (preferred for long-running services)
- **Serverless:** AWS Lambda + API Gateway (preferred for event-driven workloads)
- **Decision Criteria:**
  - Use containers for stateful or long-running processes
  - Use serverless for short-lived, event-driven, or low-traffic endpoints

## Cloud Platform

- **Provider:** AWS
- **Infrastructure as Code:** Terraform or AWS CDK
- **Key Services:**
  - Compute: ECS Fargate / AWS Lambda
  - Database: Amazon RDS (PostgreSQL) / Aurora PostgreSQL
  - Cache: Amazon ElastiCache (Redis)
  - Storage: Amazon S3
  - CDN: Amazon CloudFront
  - DNS: Amazon Route 53
  - Secrets: AWS Secrets Manager
  - Monitoring: Amazon CloudWatch
  - CI/CD: AWS CodePipeline or GitHub Actions

## Conventions

- Use ES Modules (`import/export`) not CommonJS
- Use `async/await` over raw Promises
- All environment config via environment variables (never hardcoded)
- Prefer composition over inheritance
- Write small, focused functions with single responsibility
- All API responses use consistent JSON envelope: `{ data, error, meta }`
