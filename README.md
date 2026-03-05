# Internal Developer Portal (IDP) | Backstage
A professional-grade Developer Portal built on Spotify's Backstage, providing a unified interface for software cataloging, automated scaffolding, and centralized technical documentation.

## Core Capabilities
Software Catalog: Centralized management of services, APIs, and resources.

Software Templates (Scaffolder): Automated "Golden Path" creation for Go Services, including automatic GitHub repository initialization and Catalog registration.

TechDocs-as-Code: Documentation generated locally using MkDocs and served seamlessly through the portal UI.

CI/CD Integration: Real-time visibility into GitHub Actions workflows directly within the component dashboard.

Secure Authentication: Integrated GitHub OAuth 2.0 for secure user identity and access management.

## Technical Stack
Frontend: React, Material UI, TypeScript.

Backend: Node.js, Knex.js.

Database: PostgreSQL 16 (Running via Docker).

Infrastructure: WSL2 (Ubuntu), Docker, MkDocs.

Integrations: GitHub API, GitHub Actions, TechDocs.

## Setup & Architecture
1. Database Layer
The portal relies on a persistent PostgreSQL instance. Connection stability is managed via custom ```knexConfig``` to handle WSL-to-Docker network latency.

```
docker run -d --name backstage-db -p 5432:5432 postgres:16-alpine
```

2. Authentication
Configured via GitHub OAuth App to enable secure sign-in and facilitate Scaffolder actions on behalf of the user.

3. Entity Life Cycle
The portal follows the "Fetch, Publish, Register" pattern:

Fetch: Pulls a Go service skeleton from local templates.

Publish: Creates a new repository on GitHub under the ```aashiruu``` organization.

Register: Automatically creates the ```catalog-info.yaml``` link to track the new service in the IDP.

## How to Run
1. Export Secrets:

```
export GITHUB_TOKEN=your_token
```
```
export AUTH_GITHUB_CLIENT_ID=your_id
```
```
export AUTH_GITHUB_CLIENT_SECRET=your_secret
```

2. Install Dependencies:

```
yarn install
```
3. Start the Engine:

```
yarn dev
```
## Proof of Work: Key Milestones Achieved
Local TechDocs Generation: Successfully bypassed common Docker-in-Docker issues by implementing a local mkdocs build runner.

Custom Entity Pages: Modified EntityPage.tsx to include conditional CI/CD tabs and Kubernetes observability.

Database Resilience: Resolved KnexTimeoutErrors by tuning connection pool parameters for high-latency environments.

<img width="1315" height="596" alt="image" src="https://github.com/user-attachments/assets/75aab3e7-96b7-4e89-a63e-df71e0fda62c" />

<img width="971" height="561" alt="image" src="https://github.com/user-attachments/assets/15b0585f-1a09-4747-b0b3-ccc290785009" />

<img width="1090" height="454" alt="image" src="https://github.com/user-attachments/assets/8d1ba4c4-136d-4c20-a518-4ef9286eb1fa" />

<img width="1119" height="661" alt="image" src="https://github.com/user-attachments/assets/b04c9a10-5e56-4bab-a7db-d14fcea0efe1" />

<img width="1344" height="672" alt="image" src="https://github.com/user-attachments/assets/83d0d2b2-2d9a-497e-bae4-0d768da3f8d2" />
