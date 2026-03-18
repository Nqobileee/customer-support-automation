# Customer Support Automation

Intelligent support automation platform for Tribetron.

Customers email support@tribetron.com, the system ingests requests, performs AI triage, creates/updates Monday.com tickets, and manages structured customer communication with human-in-the-loop escalation for risky cases.

## Project Goals
- Listen to inbound support emails continuously.
- Send fast acknowledgement responses.
- Gather missing scope details automatically.
- Create and update Monday.com tickets.
- Maintain reply threading and ticket continuity.
- Provide AI-assisted summaries and next-step suggestions for help desk agents.
- Run with secure secrets management, Dockerized services, and Jenkins CI/CD.

## Core Workflow
1. Customer sends email to support@tribetron.com.
2. Listener service ingests message and attachments.
3. Triage service classifies intent and extracts entities.
4. Ticket sync service creates or updates Monday.com item.
5. Communication service sends acknowledgement and follow-ups.
6. Reply detection continues the same ticket thread.
7. Low-confidence or high-risk issues escalate to a human agent.

## Recommended Tech Stack
- Language: Python
- API framework: FastAPI
- AI model: Claude (Anthropic)
- Background jobs: Celery or RQ
- Queue/cache: Redis
- Database: MongoDB
- Containerization: Docker, Docker Compose
- CI/CD: Jenkins
- Integrations: SMTP email integration, Monday.com API, Claude API

## Suggested Service Layout
- listener-service: Inbound email ingestion, parsing, deduplication
- triage-service: Intent classification, entity extraction, confidence scoring
- ticket-sync-service: Monday.com item create/update and field mapping
- communication-service: Templates, outbound replies, thread-safe messaging
- orchestration-service: State machine, retries, escalation, audit coordination
- shared: Config, schemas, logging, error handling

## Key Functional Capabilities
- Automated first response with ticket reference.
- Structured communication lifecycle:
	- Received
	- Triaged
	- In progress
	- Waiting on customer
	- Resolved
	- Closed
- Intelligent understanding of customer context and urgency.
- Human override for critical or uncertain responses.
- Audit logging for automated decisions and outbound communication.

## Non-Functional Targets
- Availability target: 99.9% monthly for intake and response paths.
- Email acknowledgement latency: <= 60 seconds (P95).
- Monday.com ticket creation latency: <= 120 seconds (P95).
- Secure secret handling and role-based access control.

## CI/CD Expectations (Jenkins)
Pipeline should include:
- Lint and static analysis
- Unit tests
- Integration tests
- Dependency and image security scans
- Docker image build
- Staging deployment gate

## Containerization Expectations (Docker)
- Every service must have a Dockerfile.
- Local integration should run via Docker Compose.
- Images should be version-tagged for traceability.

## Project Documents
- SRS: [SRS.md](SRS.md)
- Step-by-step implementation plan: [IMPLEMENTATION_PLAN.md](IMPLEMENTATION_PLAN.md)

## Immediate Next Actions
1. Finalize Monday.com board schema and status taxonomy.
2. Confirm SMTP server details and credentials.
3. Scaffold service directories and shared contracts.
4. Provision MongoDB and define initial collections/indexes.
5. Add Claude API configuration and initial Jenkins pipeline with lint and test stages.

## Notes
- This repository currently contains planning artifacts first.
- Implementation scaffolding can now be generated directly from the implementation plan.