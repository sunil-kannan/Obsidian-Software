---
date: "2026-05-13"
tags: 
link:
---
# Core-Goal

> A context repo explains the project in a way that helps AI make correct code changes..

The core goal is:
- Reduce guessing.
- Increase traceability.
- Make AI aware of architecture, conventions, ownership, and workflows.
  
### Reference Docs  
- `architecture/overview.md` — System design, service boundaries, data flows  
- `architecture/service-index.md` — 192 endpoints → controller → service → DB mapping  
- `architecture/feature-map.md` — End-to-end feature lineage (13/17 complete)  
- `architecture/ui-to-backend-map.md` — UI pages → API calls → DB tables  
- `architecture/data-model.md` — Entity relationships, cross-service table overlap  
- `architecture/db-design.md` — 90+ tables, migrations, native query hotspots  
- `architecture/domain-glossary.md` — Business terminology (Promo, KPI, CFM, ARP, etc.)  
- `architecture/code-conventions.md` — Code style templates

project-nexus/
│
├── 00-Start-Here.md
├── 01-Project-Overview.md
├── 02-AI-Usage-Guide.md
├── 03-Glossary.md
├── 04-Decision-Log.md
│
├── architecture/
│   ├── 00-Architecture-Overview.md
│   ├── 01-System-Context.md
│   ├── 02-Service-Map.md
│   ├── 03-Data-Flow.md
│   ├── 04-Event-Flow.md
│   ├── 05-External-Integrations.md
│   ├── 06-Security-Auth.md
│   └── 07-Deployment-Overview.md
│
├── services/
│   ├── 00-Service-Ownership.md
│   ├── service-template.md
│   ├── app-service.md
│   ├── user-service.md
│   └── notification-service.md
│
├── api/
│   ├── 00-API-Index.md
│   ├── 01-Gateway-Routing.md
│   ├── 02-Endpoint-Standards.md
│   └── api-template.md
│
├── database/
│   ├── 00-Database-Overview.md
│   ├── 01-Table-Ownership.md
│   ├── 02-Entity-Relationship.md
│   ├── 03-Migration-Rules.md
│   └── table-template.md
│
├── features/
│   ├── 00-Feature-Map.md
│   ├── 01-Critical-Workflows.md
│   ├── feature-template.md
│   ├── login.md
│   ├── create-order.md
│   └── upload-file.md
│
├── frontend/
│   ├── 00-Frontend-Overview.md
│   ├── 01-Routes.md
│   ├── 02-State-Management.md
│   ├── 03-API-Client-Map.md
│   └── 04-Component-Rules.md
│
├── backend/
│   ├── 00-Backend-Overview.md
│   ├── 01-Coding-Standards.md
│   ├── 02-Error-Handling.md
│   ├── 03-Logging.md
│   ├── 04-Testing-Strategy.md
│   └── 05-Security-Rules.md
│
├── workflows/
│   ├── 00-Workflow-Index.md
│   ├── 01-New-Feature-Workflow.md
│   ├── 02-Bug-Fix-Workflow.md
│   ├── 03-Code-Review-Workflow.md
│   ├── 04-Release-Workflow.md
│   └── 05-Local-Setup.md
│
├── ai-prompts/
│   ├── 00-Prompt-Index.md
│   ├── 01-New-Feature-Prompt.md
│   ├── 02-Bug-Fix-Prompt.md
│   ├── 03-Code-Review-Prompt.md
│   ├── 04-Test-Generation-Prompt.md
│   └── 05-Architecture-Review-Prompt.md
│
└── optional/
    ├── project-config.yaml
    ├── local-gateway.md
    └── tool-setup.md
For Obsidian, I would start with this minimal version:
project-nexus/
├── 00-Start-Here.md
├── 01-Project-Overview.md
├── 02-AI-Usage-Guide.md
├── 03-Glossary.md
│
├── architecture/
│   ├── 00-Architecture-Overview.md
│   ├── 01-Service-Map.md
│   ├── 02-Data-Flow.md
│   └── 03-External-Integrations.md
│
├── database/
│   ├── 00-Database-Overview.md
│   └── 01-Table-Ownership.md
│
├── features/
│   ├── 00-Feature-Map.md
│   └── 01-Critical-Workflows.md
│
├── backend/
│   ├── 00-Coding-Standards.md
│   └── 01-Testing-Strategy.md
│
└── ai-prompts/
    ├── 00-Prompt-Index.md
    ├── 01-New-Feature-Prompt.md
    ├── 02-Bug-Fix-Prompt.md
    └── 03-Code-Review-Prompt.md