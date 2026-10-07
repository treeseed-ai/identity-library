---
schemaVersion: treeseed.knowledge-page/v1
id: identity-deployment-and-recovery
bookId: identity-guide
slug: deployment-and-recovery
title: Deployment, databases and recovery
summary: Shared PostgreSQL infrastructure with isolated application databases
  and coordinated restores.
status: published
visibility: public
order: 2
contributors: []
relatedBookIds: []
relatedKnowledgeIds: []
relatedNoteIds: []
relatedQuestionIds: []
relatedObjectiveIds: []
relatedProposalIds: []
relatedDecisionIds: []
guaranteeIds: []
audiences:
  primary: []
  secondary: []
  excluded: []
capabilityIds: []
routePatterns: []
resourceTypes: []
actionIds: []
keywords:
  - identity
  - sso
  - federation
  - recovery
documentationUrls: []
---

# Deployment, databases and recovery

Deployment owns Keycloak, SPIRE, TLS, bootstrap custody, database provisioning and upgrades. Identity owns authentication adapters, SDK owns public contracts, and APIs own authorization. Platform contains portable declarations and exact release composition, not infrastructure implementation or host-specific secrets.

Applications in the same installation and environment may share one PostgreSQL service. They use separate databases and owner, migration and runtime roles. Sharing a server does not mean sharing schemas, tables or credentials. Staging and production remain isolated. Only enabled applications receive allocations. Migration authority is temporary and disabled after use.

Bootstrap material must remain available independently of OpenBao so identity and vault startup cannot depend on each other cyclically. Operational provider secrets remain in vault custody. Browser session keys and workload signing keys must not enter Git, ordinary configuration, logs or OpenTofu state.

## Safe migration

Before switching a live installation, capture a coordinated application/database restore point, stop old writers, verify account and provider mappings, apply schema and authentication migration, and validate all consuming applications. Preserve local user IDs, memberships, provider IDs and resource bindings. Import only supported password hash formats; otherwise require an explicit password reset. Never link accounts solely by matching email.

A PostgreSQL major-version transition requires a tested compatible migration. Never mount an old major version's physical data directory under a new server. Recovery must restore matching application and database generations; do not run an old authentication writer against incompatible migrated data.

## Troubleshooting

Check issuer and resource audience, current principal mappings, client registration, trusted TLS, clocks, vault/bootstrap readiness and application session status. Record bounded diagnostic categories and exact release identifiers, not tokens, authorization codes, passwords or private keys. A failed authentication check must not activate a fallback password issuer.

