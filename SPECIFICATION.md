# Feature Specification: SkillSwap Local Skill Exchange Platform

**Feature Branch**: `001-skill-exchange-platform`

**Created**: 2026-09-14

**Status**: Draft

**Input**: User description: "Create a comprehensive project specification for SkillSwap, a local skill exchange platform where people trade skills without monetary transactions. Include project goals, target audience, detailed user stories (authentication, profile management, skill listing CRUD, search/filtering, messaging, reviews), acceptance criteria, and API endpoint definitions."

## Project Overview

SkillSwap is a local, non-monetary marketplace for exchanging knowledge and practical help.
Members publish skills they can teach, discover nearby people who offer useful skills,
agree on a reciprocal exchange, communicate safely, and leave reviews after an exchange.
The platform records skill offers and exchange outcomes; it does not process payments or
assign monetary value to a skill.

### Project Goals

- Enable people to discover trustworthy local skill-sharing partners.
- Let members clearly describe skills they offer and skills they want to learn.
- Support a complete exchange journey from discovery through conversation and review.
- Make trust visible through complete profiles, exchange context, and fair reviews.
- Keep the first release focused on skill exchange rather than payments, advertising, or
  a generalized social network.

### Target Audience

- Local learners seeking practical, creative, professional, or life skills.
- People willing to teach skills in exchange for learning something from another member.
- Community members who value low-cost, reciprocal learning and local relationships.
- Users with varying technical ability who need clear, accessible, mobile-friendly workflows.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create and Secure an Account (Priority: P1)

As a new visitor, I want to create and securely access an account so that I can participate
in skill exchanges under a persistent identity.

**Why this priority**: Identity is required before users can publish offers, message others,
or build trust through reviews.

**Independent Test**: A tester can register, verify the account, sign in, sign out, and
recover access using only the authentication flow, without any other platform feature.

**Acceptance Scenarios**:

1. **Given** a visitor with a valid unused email address, **When** they submit a display
   name, email, and password meeting the stated rules, **Then** an account is created and
   the visitor is told how to verify the email address.
2. **Given** an unverified account, **When** the user follows the valid verification link,
   **Then** the account becomes active and the user can sign in.
3. **Given** an active account, **When** the user submits valid credentials, **Then** the
   platform starts an authenticated session and shows the user's signed-in state.
4. **Given** invalid credentials, **When** the user attempts to sign in, **Then** access is
   denied with a clear, non-sensitive error and no account detail is disclosed.
5. **Given** a signed-in user, **When** they choose sign out, **Then** the session is
   invalidated and protected actions require authentication again.
6. **Given** a user who cannot remember their password, **When** they request recovery for
   their email, **Then** the platform provides a time-limited reset flow without revealing
   whether the email exists.

### User Story 2 - Build a Useful Profile (Priority: P1)

As a member, I want to manage a profile that explains who I am, where I participate, and
what I can teach or want to learn so that other members can judge whether an exchange is a
good fit.

**Why this priority**: Profiles provide context and trust before two people decide to
communicate or exchange skills.

**Independent Test**: A signed-in tester can create, edit, preview, and view their profile,
including location visibility and learning interests, without publishing a skill listing.

**Acceptance Scenarios**:

1. **Given** a signed-in member with no completed profile, **When** they submit valid profile
   details, **Then** the profile is saved and the member can preview its public representation.
2. **Given** a member editing their profile, **When** they change their bio, availability,
   interests, or location-sharing choice, **Then** the updated values appear to the member
   and only the selected location detail is publicly visible.
3. **Given** a visitor viewing a member profile, **When** the profile is public, **Then** the
   visitor can see the member's display name, bio, offered skills, wanted skills, general
   location, availability, and review summary when those values exist.
4. **Given** a member submits invalid or unsafe profile content, **When** they save it,
   **Then** the platform rejects the invalid fields with actionable validation messages.

### User Story 3 - Manage Offered and Wanted Skills (Priority: P1)

As a member, I want to create, view, edit, and remove skill listings so that my offers and
learning goals stay accurate.

**Why this priority**: Skill listings are the core inventory that makes reciprocal matching
possible.

**Independent Test**: A signed-in tester can perform the full create, read, update, and
delete lifecycle for both an offered skill and a wanted skill.

**Acceptance Scenarios**:

1. **Given** a signed-in member, **When** they create an offered skill with a title,
   description, category, experience level, and availability, **Then** the listing is saved
   as active and associated with that member.
2. **Given** an active skill listing owned by the member, **When** they edit its details,
   **Then** future viewers see the updated values and the listing keeps its identity.
3. **Given** an active skill listing owned by the member, **When** they delete or archive it,
   **Then** it no longer appears in discovery results and its historical exchange references
   remain understandable.
4. **Given** a member attempts to change or delete another member's listing, **When** the
   request is submitted, **Then** the platform denies the action.
5. **Given** a listing with missing required fields or unsupported values, **When** it is
   submitted, **Then** the platform rejects it without creating a partial listing.

### User Story 4 - Discover and Filter Local Matches (Priority: P1)

As a learner, I want to search and filter skill listings so that I can find relevant local
people without scanning unrelated results.

**Why this priority**: Discovery connects a member's learning goal to a possible exchange
partner and is the primary route into the platform.

**Independent Test**: A tester can search by keyword and apply location, category, skill
level, availability, and listing type filters, then open a result profile.

**Acceptance Scenarios**:

1. **Given** published listings exist, **When** a visitor searches for a keyword, **Then**
   results include matching titles, descriptions, or categories and provide a useful empty
   state when there are no matches.
2. **Given** search results, **When** the visitor selects a category, listing type, level,
   availability, or distance filter, **Then** every visible result satisfies the selected
   filters.
3. **Given** a visitor has chosen a location, **When** the visitor searches nearby, **Then**
   results are ordered by relevance and local proximity without exposing a precise address.
4. **Given** a result belongs to the current user, **When** discovery results load, **Then**
   the platform identifies it as the user's own listing and does not create a self-match.
5. **Given** a visitor is not signed in, **When** they browse public listings, **Then** they
   can view discovery results but are prompted to authenticate before contacting a member.

### User Story 5 - Message a Potential Exchange Partner (Priority: P2)

As a member, I want to start and continue a private conversation about a specific skill
exchange so that both people can agree on expectations and timing without money changing hands.

**Why this priority**: Messaging turns a promising match into a coordinated, consensual
exchange while preserving a clear non-monetary scope.

**Independent Test**: Two test accounts can start a conversation from a listing, exchange
messages, view unread state, and report or block a conversation participant.

**Acceptance Scenarios**:

1. **Given** an authenticated member viewing another member's listing, **When** they send a
   message referencing the listing, **Then** a private conversation is created and the
   recipient can see the message.
2. **Given** an existing conversation, **When** a participant sends a non-empty message,
   **Then** it appears in chronological order with sender and timestamp information.
3. **Given** a participant has unread messages, **When** they open the conversation, **Then**
   those messages are marked read and the unread count is updated.
4. **Given** a participant has blocked or reported the other participant, **When** either
   person attempts further contact, **Then** the platform prevents new messages according to
   the safety action and confirms the outcome without exposing private report details.
5. **Given** a message contains prohibited or unsupported content, **When** it is submitted,
   **Then** the platform rejects it and explains the applicable content rule.

### User Story 6 - Confirm an Exchange and Leave a Review (Priority: P2)

As a member who completed a skill exchange, I want to record the outcome and leave a fair
review so that future members can make informed trust decisions.

**Why this priority**: Reviews create accountability and useful trust signals, but they
require an exchange context and therefore follow discovery and messaging.

**Independent Test**: Two test accounts can mark an exchange complete, each submit one review,
and view the resulting review summary on the other member's profile.

**Acceptance Scenarios**:

1. **Given** two members have agreed through a conversation, **When** one member records an
   exchange with the offered and requested skills, **Then** the other member can confirm or
   dispute the exchange record.
2. **Given** both members have confirmed a completed exchange, **When** either member submits
   a rating and optional written review, **Then** the review is stored and attributed to the
   completed exchange.
3. **Given** a member has already reviewed a completed exchange, **When** they submit another
   review for the same exchange, **Then** the platform rejects the duplicate and preserves
   the original review.
4. **Given** a profile has one or more published reviews, **When** another member views it,
   **Then** the platform shows the aggregate rating, count, and review content subject to
   moderation and visibility rules.
5. **Given** a member flags a review as abusive, private, or inaccurate, **When** the report
   is submitted, **Then** the review is queued for moderation and the reporter receives a
   confirmation.

### Edge Cases

- Registration with an already-used email MUST return a safe, actionable error without
  exposing account ownership details.
- A verification, password-reset, or message action using an expired or invalid token MUST
  fail safely and offer a way to restart the flow.
- A user changing their profile location MUST not expose a street address or exact device
  location; public results use a general area and optional distance.
- Deleting a listing with historical exchanges MUST archive the listing from discovery while
  preserving the exchange and review context.
- Search MUST handle empty queries, unsupported filter combinations, pagination beyond the last
  page, and no-result states without returning an error page.
- A user MUST not be able to message themselves, review an exchange they did not participate
  in, or submit more than one review for the same completed exchange.
- Concurrent edits to a listing or profile MUST not silently overwrite a newer saved value.
- The platform MUST reject blank, oversized, or unsafe message and review content.
- A reported or blocked account MUST not bypass the restriction by starting a new conversation.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow a visitor to register with a unique email address, display
  name, and password, then verify the email before protected actions are enabled.
- **FR-002**: System MUST support sign in, sign out, password recovery, password reset, and
  session expiry while avoiding account-enumeration disclosures.
- **FR-003**: System MUST enforce password rules and validate all user-submitted fields with
  actionable messages before persistence.
- **FR-004**: System MUST allow an authenticated member to create, read, update, and delete
  their own profile, including bio, general location, availability, offered skills, and wanted
  skills.
- **FR-005**: System MUST provide a public profile view that respects profile visibility and
  location-sharing choices.
- **FR-006**: System MUST allow an authenticated member to create, read, update, archive, and
  delete offered or wanted skill listings with title, description, category, level, type, and
  availability fields.
- **FR-007**: System MUST prevent users from modifying or deleting resources they do not own.
- **FR-008**: System MUST make only active, public, and valid skill listings eligible for
  discovery results.
- **FR-009**: System MUST support keyword search and filtering by listing type, category,
  skill level, availability, general location, and distance when location is provided.
- **FR-010**: System MUST provide pagination, stable result ordering, result counts or clear
  continuation state, and an explicit no-results state.
- **FR-011**: System MUST allow an authenticated member to start a private conversation from
  another member's listing and send messages tied to the potential exchange.
- **FR-012**: System MUST display conversations in chronological order, track unread messages,
  and prevent messages after a relevant block or safety restriction.
- **FR-013**: System MUST provide report and block actions for members, messages, and reviews,
  and MUST prevent reporters' private details from being exposed to the reported party.
- **FR-014**: System MUST allow participants to record and confirm a completed skill exchange
  without collecting or displaying a monetary price.
- **FR-015**: System MUST allow each participant to submit at most one rating and review for a
  completed exchange and MUST show aggregate review information on eligible profiles.
- **FR-016**: System MUST support review reporting and moderation status without silently
  changing review content or attribution.
- **FR-017**: System MUST return consistent validation, authentication, authorization, not-found,
  conflict, rate-limit, and server-error responses for API consumers.
- **FR-018**: System MUST protect private messages, authentication data, and non-public profile
  fields from unauthenticated or unauthorized access.
- **FR-019**: System MUST provide keyboard-accessible, readable, responsive states for loading,
  empty results, validation errors, unavailable content, and recoverable failures.
- **FR-020**: System MUST record enough audit context for authentication events, ownership
  changes, reports, exchange confirmations, and review submissions to support safety inquiries.

### API Endpoint Definitions

The API is versioned under `/api/v1`. JSON request and response bodies use resource-specific
objects. Successful create operations return `201`, successful reads and updates return `200`,
successful deletes or sign-outs return `204` when no response body is needed. Errors use a
consistent shape: `{ "error": { "code": "...", "message": "...", "fields": {} } }`.
Authentication is represented by the current signed-in session; protected endpoints return
`401` when no session exists and `403` when the session lacks permission.

#### Authentication

| Method and path | Purpose | Authentication | Request | Success and failures |
| --- | --- | --- | --- | --- |
| `POST /api/v1/auth/register` | Create account | Public | `displayName`, `email`, `password` | `201` with account status; `400` validation; `409` duplicate email |
| `POST /api/v1/auth/verify-email` | Verify email | Public token | `token` | `200` verified status; `400` invalid or expired token |
| `POST /api/v1/auth/login` | Start session | Public | `email`, `password` | `200` current user; `401` invalid credentials; `429` rate limit |
| `POST /api/v1/auth/logout` | End session | Required | None | `204`; `401` if no active session |
| `POST /api/v1/auth/password/forgot` | Start recovery | Public | `email` | `202` generic acknowledgement regardless of account existence |
| `POST /api/v1/auth/password/reset` | Set new password | Public token | `token`, `password` | `200`; `400` invalid token or password |
| `GET /api/v1/auth/me` | Get current user | Required | None | `200` account summary; `401` unauthenticated |

#### Profiles

| Method and path | Purpose | Authentication | Request or query | Success and failures |
| --- | --- | --- | --- | --- |
| `GET /api/v1/profiles/:userId` | View public profile | Public, subject to visibility | None | `200` public profile; `404` unavailable user |
| `GET /api/v1/me/profile` | View own full profile | Required | None | `200` profile including private settings |
| `PATCH /api/v1/me/profile` | Update own profile | Required | Partial profile fields | `200` updated profile; `400` validation; `409` stale update |
| `DELETE /api/v1/me/profile` | Request account deletion | Required | Optional confirmation | `202` deletion state; `401` unauthenticated |

#### Skill Listings and Discovery

| Method and path | Purpose | Authentication | Request or query | Success and failures |
| --- | --- | --- | --- | --- |
| `POST /api/v1/skills` | Create offered or wanted listing | Required | `type`, `title`, `description`, `category`, `level`, `availability`, `area` | `201`; `400` validation |
| `GET /api/v1/skills/:skillId` | View listing | Public if active | None | `200`; `404` unavailable listing |
| `PATCH /api/v1/skills/:skillId` | Update owned listing | Required, owner | Partial listing fields | `200`; `403` not owner; `409` stale update |
| `DELETE /api/v1/skills/:skillId` | Archive owned listing | Required, owner | None | `204`; `403` not owner; `404` missing |
| `GET /api/v1/skills` | Search and filter listings | Public | `q`, `type`, `category`, `level`, `availability`, `area`, `distance`, `page`, `limit`, `sort` | `200` paginated results; `400` invalid filters |
| `GET /api/v1/me/skills` | List current user's listings | Required | `status`, `type`, pagination | `200`; `401` unauthenticated |

#### Messaging and Safety

| Method and path | Purpose | Authentication | Request or query | Success and failures |
| --- | --- | --- | --- | --- |
| `POST /api/v1/conversations` | Start conversation from listing | Required | `recipientId`, `skillId`, `message` | `201`; `400` invalid content; `409` blocked or self-contact |
| `GET /api/v1/conversations` | List own conversations | Required | `page`, `limit`, `unreadOnly` | `200` conversation summaries |
| `GET /api/v1/conversations/:conversationId/messages` | Read conversation messages | Required, participant | `before`, `limit` | `200`; `403` not participant; `404` missing |
| `POST /api/v1/conversations/:conversationId/messages` | Send message | Required, participant | `body` | `201`; `403` restricted; `429` rate limit |
| `POST /api/v1/conversations/:conversationId/read` | Mark messages read | Required, participant | None | `204`; `403` not participant |
| `POST /api/v1/users/:userId/block` | Block member | Required | Optional `reason` | `204`; `409` self-block |
| `DELETE /api/v1/users/:userId/block` | Unblock member | Required | None | `204`; `404` no block exists |
| `POST /api/v1/reports` | Report member, message, listing, or review | Required | `targetType`, `targetId`, `reason`, optional `details` | `201`; `400` invalid target or reason |

#### Exchanges and Reviews

| Method and path | Purpose | Authentication | Request or query | Success and failures |
| --- | --- | --- | --- | --- |
| `POST /api/v1/exchanges` | Record an agreed exchange | Required, participants | `partnerId`, `offeredSkillId`, `wantedSkillId`, `summary` | `201`; `409` invalid partner or duplicate exchange |
| `GET /api/v1/exchanges` | List own exchanges | Required | `status`, pagination | `200` exchanges for current user only |
| `POST /api/v1/exchanges/:exchangeId/confirm` | Confirm completion | Required, participant | None | `200`; `403` not participant; `409` already resolved |
| `POST /api/v1/exchanges/:exchangeId/dispute` | Dispute exchange details | Required, participant | `reason` | `202`; `400` missing reason |
| `POST /api/v1/exchanges/:exchangeId/reviews` | Submit one review | Required, confirmed participant | `rating`, optional `comment` | `201`; `409` duplicate or unconfirmed exchange |
| `GET /api/v1/users/:userId/reviews` | View eligible reviews | Public subject to visibility | `page`, `limit` | `200` review list and aggregate |
| `POST /api/v1/reviews/:reviewId/report` | Report a review | Required | `reason`, optional `details` | `201`; `404` unavailable review |

### API Contract Rules

- API responses MUST exclude passwords, reset tokens, private report details, exact addresses,
  and any other non-public profile fields unless the authenticated owner is requesting them.
- List endpoints MUST document pagination limits and MUST cap the maximum page size.
- Mutating endpoints MUST validate ownership, participant status, resource state, and content
  before applying changes.
- Authentication, messaging, reporting, and review submission endpoints MUST be rate-limited
  and MUST return a retry-safe error response when a limit is reached.
- Endpoint behavior MUST remain consistent with the acceptance scenarios above; changes to a
  resource contract require updating this specification and affected clients.

### Key Entities

- **User**: An account holder with verified identity state, display name, credentials, safety
  status, and timestamps.
- **Profile**: Public and private information about a user, including bio, general area,
  availability, interests, and visibility choices.
- **SkillListing**: A user's offered or wanted skill with title, description, category, level,
  availability, general area, lifecycle status, and owner.
- **Conversation**: A private exchange discussion between two users, optionally linked to a
  skill listing, with participant and unread state.
- **Message**: A timestamped piece of conversation content with sender, recipient context,
  moderation state, and read state.
- **Exchange**: A non-monetary agreement between participants describing the skills exchanged,
  confirmation state, dispute state, and completion timestamps.
- **Review**: A rating and optional comment authored by an exchange participant and attached to
  one confirmed exchange, with moderation and visibility state.
- **Report**: A safety or moderation request concerning a user, listing, message, or review,
  including reporter, target, reason, status, and audit timestamps.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: At least 90% of first-time testers can register, verify their account, and sign
  in without assistance within 3 minutes.
- **SC-002**: At least 85% of testers can publish a complete offered skill listing within 5
  minutes of signing in.
- **SC-003**: At least 90% of valid searches return a relevant, filter-compliant result or a
  clear no-results state within 2 seconds under the agreed pilot load.
- **SC-004**: At least 80% of testers can identify and open a suitable local skill listing
  within 3 minutes using keyword search and filters.
- **SC-005**: At least 90% of messages sent between test participants are delivered once and
  appear in the correct chronological conversation within 5 seconds under normal conditions.
- **SC-006**: At least 90% of completed exchanges can be confirmed and reviewed without support
  intervention, with duplicate reviews rejected.
- **SC-007**: 100% of protected endpoint scenarios in the acceptance tests reject unauthenticated
  or unauthorized access and expose no protected profile or message data.
- **SC-008**: In usability review, users rate the core discovery-to-contact journey at least 4
  out of 5 for clarity and confidence, and no critical accessibility blocker remains open.

## Assumptions

- The first release is a responsive web experience; native mobile applications are out of
  scope.
- The service operates in one pilot community or region, with a general area used instead of
  precise addresses.
- Email is available for account verification and password recovery; the specific delivery
  provider is an implementation decision for planning.
- Users are expected to agree on exchange timing and exact meeting details privately; SkillSwap
  records the exchange context but does not provide payment, calendar, video, or transport
  services in this scope.
- Moderation is available to review reports before an account or review is permanently removed.
- A listing owner and a potential partner may communicate only after authentication; public
  discovery remains available to signed-out visitors.
- Search results are initially limited to active listings and a reasonable pilot dataset; any
  future recommendation or ranking model is outside this specification.
- All exchanges are voluntary and non-monetary. The platform does not calculate, require, or
  display a cash price or monetary balance.
