---
inclusion: manual
---

# Optional TypeScript, React, and AWS Technology Profile

> [!NOTE]
> This is an opinionated profile for teams that have selected this stack. Reference it manually; do
> not use it to override an existing repository's architecture, approved technology standards, or
> workload constraints.

## Backend

- **Runtime and language:** Node.js with TypeScript in strict mode
- **Framework:** Express or Fastify; choose from measured needs and team supportability
- **API style:** REST or GraphQL according to the product contract
- **Runtime validation:** Zod or the validation library already established by the project

## Frontend

- **Framework:** React with TypeScript
- **Build tool:** Vite
- **Styling:** Tailwind CSS when it matches the product's design-system approach
- **Server state:** TanStack Query
- **Client state:** Local React state first; Zustand when shared client state warrants it
- **Routing:** The current supported React Router release selected by the project

## Data and caching

- **Relational database:** PostgreSQL, Amazon RDS for PostgreSQL, or Aurora PostgreSQL
- **Data access:** Prisma or the query tool already established by the project
- **Cache and messaging:** Amazon ElastiCache for Valkey or Redis OSS when a measured requirement
  justifies caching, rate limiting, session storage, or pub/sub
- **Migrations:** Version and review schema changes with the application's migration tooling

## AWS deployment options

Choose from workload requirements rather than a universal default:

| Pattern | Good fit | Important considerations |
| --- | --- | --- |
| AWS Lambda and API Gateway | Event-driven or request-driven work with bounded execution | Cold starts, service quotas, timeout, concurrency, and externalized durable state |
| Containers on ECS Fargate | Long-running services, workers, or workloads needing container-level control | Scaling, health checks, patching, image lifecycle, and load balancing |

Keep durable application state outside compute instances for both patterns. Evaluate availability,
latency, traffic shape, operational skills, security, and cost before choosing.

## Infrastructure and delivery

- **Infrastructure as code:** Use the organization's supported option: AWS SAM, CloudFormation, AWS
  CDK, or Terraform.
- **Common services:** Amazon S3, CloudFront, Route 53, Secrets Manager, and CloudWatch as required.
- **CI/CD:** AWS CodePipeline, GitHub Actions, or the delivery platform approved for the repository.
- **Configuration:** Store environment-specific configuration outside source code; never hard-code
  secrets.

## Coding conventions

- Follow conventions already present in the repository before applying this profile.
- Prefer ES modules and `async`/`await` when supported by the selected runtime and build system.
- Prefer composition over inheritance where it keeps behavior easier to test and understand.
- Keep functions focused, but do not split code solely to satisfy an arbitrary size target.
- Define API response and error shapes in the API contract; apply them consistently once selected.
