<!--
Sync Impact Report
- Version change: scaffold/unversioned -> 1.0.0
- Modified principles: placeholder principles -> Product Value; Strict Type Safety;
	App Router Rendering Discipline; Verification Before Integration; Inclusive,
	Maintainable Delivery
- Added sections: Technology Standards; Team Workflow and Collaboration
- Removed sections: none
- Follow-up TODOs: confirm the historical ratification date if the team has one
-->

# SkillSwap Constitution

## Core Principles

### I. Product Value and User Trust
Every feature MUST support SkillSwap's core purpose: helping people discover,
exchange, and benefit from skills. Requirements and implementation decisions MUST
prioritize clear user outcomes, understandable interfaces, accessibility, and
responsible handling of user data. Unneeded complexity and speculative features
MUST be rejected until a concrete user need is documented.

### II. Strict Type Safety
All application code MUST use TypeScript in strict mode. The codebase MUST NOT
introduce `any`; unknown external data MUST be narrowed or validated before use.
Public functions, component props, API payloads, and shared data models MUST have
explicit, meaningful types. Type errors MUST be resolved rather than suppressed,
because compile-time contracts reduce runtime defects and make collaboration safer.

### III. App Router Rendering Discipline
SkillSwap MUST use Next.js App Router conventions. Components MUST remain Server
Components by default. A component MAY use the `use client` directive only when it
requires browser APIs, local state, effects, event handlers, or a client-only
library. Server Components MUST own data fetching and secrets; Client Components
MUST receive only the serializable data and callbacks they need. Server-only code
MUST NOT be imported into Client Components, and interactive boundaries MUST be
kept as small as practical to preserve performance and security.

### IV. Verification Before Integration
Every change MUST pass the relevant typecheck, lint, and test or build checks
before merge. New behavior and bug fixes MUST include focused automated coverage
when the behavior can be tested. Changes affecting routes, shared types, data
contracts, authentication, or rendering boundaries MUST include integration-level
verification. A failing check MUST be fixed or explicitly documented in the pull
request; it MUST NOT be hidden by disabling a rule or weakening a test.

### V. Inclusive, Maintainable Delivery
Code MUST be organized around clear ownership and small, reviewable changes.
User-facing flows MUST account for keyboard access, readable content, responsive
layouts, and meaningful loading, error, and empty states. Shared abstractions MUST
be introduced only when they clarify repeated behavior. Documentation, naming,
and commit or pull request context MUST be sufficient for another teammate to
understand and safely maintain the change.

## Technology Standards

The required application stack is Next.js using the App Router, TypeScript in
strict mode, and Tailwind CSS used through utility classes. New styling MUST use
Tailwind utilities and existing project conventions; ad hoc style systems MUST
not be introduced without an approved exception. ESLint and Prettier are the
standard static analysis and formatting tools. Formatting MUST be applied before
review, and lint configuration MUST remain compatible with Prettier. Dependencies
MUST be justified by a concrete need and kept current enough to receive security
updates. Secrets MUST remain outside source control and server-only credentials
MUST never cross a Client Component boundary.

## Team Workflow and Collaboration

SkillSwap is maintained by Ifeanyi Eme, Armando Martin Fernandez Jara, Brandon
Arroyo, and Michael Earl Kyne. Each change MUST have one clear owner, a focused
branch or pull request, and a description of the user impact, implementation
choices, verification performed, and any known follow-up work. Pull requests
MUST receive review from at least one other team member; changes to shared types,
authentication, data access, or application-wide layout SHOULD receive two
reviewers. Reviewers MUST assess correctness, type safety, rendering boundaries,
accessibility, tests, and maintainability rather than only visual output.

The author is responsible for resolving feedback and keeping the branch
rebasable or mergeable. Reviewers MUST be respectful, specific, and timely.
Conflicting technical decisions MUST be documented in the pull request and
resolved by team discussion, with the final rationale recorded when it affects
future work. No teammate may merge their own change without the required review
and passing quality checks.

## Governance

This constitution is the highest-level project standard for SkillSwap. Every pull
request MUST comply with it or document a narrowly scoped exception, its reason,
its risk, and its expiration or replacement plan. Amendments require a pull
request, review by at least two team members, and an updated Sync Impact Report.
The team MUST update dependent specifications, plans, or tasks when an amendment
changes implementation constraints.

The constitution uses semantic versioning: MAJOR for incompatible governance
changes or removals, MINOR for new principles or materially expanded obligations,
and PATCH for clarifications that do not change obligations. Compliance is
reviewed during every pull request and at each release milestone. The constitution
owner or designated reviewer MUST resolve violations before release unless an
approved exception is recorded.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): historical adoption date unknown | **Last Amended**: 2026-09-14
