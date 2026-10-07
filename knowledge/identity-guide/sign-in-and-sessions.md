---
schemaVersion: treeseed.knowledge-page/v1
id: identity-sign-in-and-sessions
bookId: identity-guide
slug: sign-in-and-sessions
title: Sign-in and application sessions
summary: One identity session, separate application sessions and permissions.
status: published
visibility: public
order: 0
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

# Sign-in and application sessions

TreeSeed's Identity architecture uses Keycloak for human sign-in. Admin, Market, CLI authorization, and registered applications use separate OAuth clients. A successful identity-provider session can avoid another password prompt, but applications do not share cookies or permissions.

Applications redirect to the identity provider instead of collecting passwords. Browser access and refresh tokens belong in the API-backed encrypted session store; the browser receives only an opaque, Secure, HttpOnly, host-only session cookie. State, nonce, PKCE, exact redirects and same-origin logout protect the sign-in flow.

Signing in does not add you to a team, make you an owner, or authorize marketplace or assignment operations. API permissions remain in each installation's database. Accounts are mapped by issuer and subject, never automatically merged by email.

Default logout ends the current application session. Identity-wide logout is a separate operation that must use the provider's supported session mechanisms. Do not assume closing one app signs you out everywhere.

## Rollout boundary

These pages describe the accepted architecture, not a claim that every installed application has migrated. Consult Platform's accepted composition and Identity delivery issue for installation status. Adapter acceptance alone is not full application acceptance.

