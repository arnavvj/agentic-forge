# 02. Software Architecture Design

> **Owner:** User / project director. **Purpose:** Capture the approved full-stack software architecture and important boundaries. **Editing rule:** Claude must treat this file as read-only unless explicitly asked to edit it.

Use checkboxes to select options. For single-choice groups, select one option. Add `Other` or a short explanation when needed. An unchecked option is not an approval.

## 1. Architecture overview

### System summary
Describe the major components and how requests and data move through the system.

_Write here:_

### Architecture style
- [ ] Modular monolith
- [ ] Service-oriented architecture
- [ ] Microservices
- [ ] Serverless
- [ ] Client-heavy application with backend APIs
- [ ] Other:

**Why this style fits:**

### Component map

| Component | Responsibility | Runs where | Calls / depends on |
|---|---|---|---|
| Frontend | | | |
| Backend / API | | | |
| Agentic service (if applicable) | | | |
| Background worker (if applicable) | | | |
| Other | | | |

### Architecture diagram (optional)
```text
Add diagram or describe the flow here.
```

## 2. Frontend

- **Application type:** [ ] Web app [ ] Mobile app [ ] Desktop app [ ] CLI [ ] API only [ ] Other:
- **Framework / language:** [ ] React [ ] Next.js [ ] Vue [ ] Svelte [ ] Angular [ ] Flutter [ ] Native [ ] Other:
- **Rendering / interaction:** [ ] Client-rendered [ ] Server-rendered [ ] Static [ ] Mixed [ ] Not applicable
- **UI component approach:** [ ] Existing component library [ ] Custom components [ ] Minimal UI [ ] Other:
- **State management:**
- **Streaming / real-time UI:** [ ] Not needed [ ] Server-Sent Events (SSE) [ ] WebSockets [ ] Polling [ ] Other:
- **Accessibility or responsive requirements:**

## 3. Backend and API

- **Backend language / framework:** [ ] Python [ ] TypeScript / Node.js [ ] Java [ ] Go [ ] .NET [ ] Other:
- **API style:** [ ] REST [ ] GraphQL [ ] gRPC [ ] RPC / actions [ ] Other:
- **API contract:** [ ] OpenAPI [ ] Schema-first [ ] Code-first [ ] Other:
- **Backend structure:** [ ] Modular application [ ] Multiple services [ ] Serverless functions [ ] Other:
- **Validation and error format:**
- **Rate limiting / request limits:**
- **API versioning needs:**

## 4. Data storage

### Primary data store
- [ ] PostgreSQL
- [ ] MySQL
- [ ] SQLite
- [ ] MongoDB
- [ ] Managed cloud database
- [ ] Other:
- **Reason / data model notes:**

### Additional storage
- **Cache:** [ ] None [ ] Redis [ ] In-process [ ] Managed cache [ ] Other:
- **Search / vector retrieval:** [ ] None [ ] PostgreSQL extension [ ] Dedicated vector store [ ] Search service [ ] Other:
- **Object / file storage:** [ ] None [ ] Local for MVP [ ] S3-compatible [ ] Cloud object storage [ ] Other:
- **Analytics / event store:**
- **Backup and restore expectations:**

## 5. Identity, authorization, and tenancy

- **Authentication:** [ ] None for local demo [ ] Email / password [ ] OAuth / social login [ ] Enterprise SSO [ ] Managed identity provider [ ] Other:
- **Authorization:** [ ] No protected roles [ ] Role-based access control (RBAC) [ ] Attribute-based access control (ABAC) [ ] Resource ownership checks [ ] Other:
- **Roles / permissions:**
- **Tenant model:** [ ] Single-user / single-tenant [ ] Shared single tenant [ ] Multi-tenant [ ] Not applicable
- **Data isolation approach:**
- **Admin / privileged operations:**
- **Session and token handling:**

## 6. External integrations

| Integration / provider | Purpose | Interface | Required for MVP? | Failure behavior |
|---|---|---|---|---|
| | | [ ] API [ ] SDK [ ] MCP [ ] Webhook [ ] Other | [ ] Yes [ ] No | |
| | | [ ] API [ ] SDK [ ] MCP [ ] Webhook [ ] Other | [ ] Yes [ ] No | |

- **External API credentials and secret management:**
- **Mock / sandbox option for development:**
- **Webhook verification or callback security:**

## 7. Request execution and background work

- **Primary request pattern:** [ ] Synchronous request / response [ ] Streaming response [ ] Background job [ ] Mixed
- **Long-running work:** [ ] Not needed [ ] In-process background task [ ] Queue + worker [ ] Durable workflow engine [ ] Other:
- **Queue / job technology:** [ ] Framework-native [ ] Managed queue [ ] Redis-backed queue [ ] RabbitMQ [ ] Kafka / event streaming [ ] Other:
- **Durable workflow engine:** [ ] Not needed [ ] Temporal [ ] Inngest [ ] Trigger.dev [ ] Cloud workflow service [ ] Other:
- **Persistence / recovery needs:** [ ] Not needed [ ] Persist job status [ ] Checkpoint and resume [ ] Durable execution history [ ] Other:
- **Retries, timeouts, and cancellation:**
- **Idempotency requirements:** Which actions must not happen twice?

**Design notes:** A normal short request does not automatically need a durable workflow engine. Long-running work that must survive restarts, wait for people or timers, or resume after failure may need durable orchestration.

## 8. Deployment and environments

- **Development:** [ ] Local only [ ] Containers [ ] Shared dev environment [ ] Other:
- **Hosting:** [ ] Vercel [ ] AWS [ ] Azure [ ] GCP [ ] Fly.io [ ] Render [ ] Railway [ ] Self-hosted [ ] Other:
- **Deployment model:** [ ] Single application [ ] Containers [ ] Serverless [ ] Multiple services [ ] Other:
- **Environments:** [ ] Local [ ] Development [ ] Staging [ ] Production [ ] Other:
- **CI / CD:** [ ] None for MVP [ ] Basic automated checks [ ] Build and deploy pipeline [ ] Other:
- **Infrastructure as code:** [ ] Not needed for MVP [ ] Required [ ] Later [ ] Other:
- **Environment configuration and secrets:**

## 9. Security, privacy, and reliability

- [ ] Validate inputs at trust boundaries.
- [ ] Enforce authorization on the server, not only in the UI or model instructions.
- [ ] Protect tenant and resource data from cross-access.
- [ ] Store secrets outside source control.
- [ ] Use secure transport and appropriate encryption at rest.
- [ ] Apply upload, file type, and file size restrictions where relevant.
- [ ] Protect against common web and API security risks.
- [ ] Add audit logs for important actions.
- [ ] Define data retention and deletion behavior.
- [ ] Add backups and recovery procedures where required.
- [ ] Other:

**Project-specific security / privacy notes:**

## 10. Observability and operations

- **Logging:** [ ] Basic application logs [ ] Structured logs [ ] Centralized logging [ ] Other:
- **Metrics:** [ ] Not needed for MVP [ ] Basic health metrics [ ] Service metrics [ ] Business metrics [ ] Other:
- **Tracing:** [ ] Not needed for MVP [ ] Request tracing [ ] Distributed tracing [ ] Agent / workflow tracing [ ] Other:
- **Error monitoring:** [ ] Console / logs [ ] Error reporting service [ ] Other:
- **Health checks / status endpoint:**
- **Alerts or operational response needs:**

## 11. Quality and testing

- **Backend tests:** [ ] Unit [ ] Integration [ ] API / contract [ ] End-to-end [ ] Other:
- **Frontend tests:** [ ] Component [ ] Integration [ ] Browser end-to-end [ ] Other:
- **Data / migration tests:**
- **Security / permission tests:**
- **Load / performance tests:** [ ] Not for MVP [ ] Required [ ] Later
- **Critical paths that must be tested:**

## 12. Performance and scale

- **Expected initial users / workload:**
- **Expected growth:**
- **Target response time / latency:**
- **Throughput / concurrency needs:**
- **Availability / recovery targets:**
- **Known bottlenecks or constraints:**

## 13. Approved technology choices

| Area | Approved choice | Flexibility |
|---|---|---|
| Frontend | | [ ] Fixed [ ] Suggest alternatives |
| Backend | | [ ] Fixed [ ] Suggest alternatives |
| Database | | [ ] Fixed [ ] Suggest alternatives |
| Hosting | | [ ] Fixed [ ] Suggest alternatives |
| Agent framework (if applicable) | | [ ] Fixed [ ] Suggest alternatives |
| Other | | [ ] Fixed [ ] Suggest alternatives |

## 14. Open questions and trade-offs

| Question / trade-off | Options considered | Current direction | Needs director approval? |
|---|---|---|---|
| | | | [ ] Yes [ ] No |

---

**Director sign-off:** [ ] This software design is ready for planning.

Claude may recommend changes separately, but a material architecture change requires your approval and should be recorded in `docs/06-DECISIONS.md`.
