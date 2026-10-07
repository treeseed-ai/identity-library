---
schemaVersion: treeseed.knowledge-page/v1
id: identity-federation-and-workloads
bookId: identity-guide
slug: federation-and-workloads
title: Federation and workload trust
summary: Directional trust, audience-bound credentials, and separate machine
  authorization.
status: published
visibility: public
order: 1
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

# Federation and workload trust

A private installation remains sovereign. Its local sign-in must work without TreeSeed central. Federation connects explicitly approved identity providers in one direction: trusting a provider does not automatically trust providers that it trusts.

Operators must specify permitted issuers, applications, released claims and assurance requirements. Trust removal must block new authentication and invalidate affected sessions and exchanges. Federation does not copy private team content, grant team membership or connect private APIs.

Workload identity is separate from human sign-in. Managed Linux uses SPIRE attestation where supported; environments without proven node attestation use independently provisioned asymmetric workload keys. A bootstrap key proves key possession, not hardware attestation. Tokens are short-lived and bound to one resource and registered principal. Never forward a Market API token to another market.

Capacity-provider enrollment and approval still establish eligibility and permissions. Kata guests receive assignment-scoped credentials, not host-wide provider credentials or a host SPIRE socket. Artifact signing, encryption and recovery keys are not login credentials.

## Scope labels are not permissions

Managed custom OAuth scopes carry requested permission labels without Keycloak role grants or claim mappers. Each API independently checks the local principal and permissions. Client registration rejects unmanaged or drifted policy instead of silently expanding authority.

