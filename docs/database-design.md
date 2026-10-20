# Database Design

**Project:** Development of a Web-Based Volunteer and Event Management System for Astana IT University: Recruitment, Intelligent Matching, and Activity Coordination

**Members:** Aitkali Ayazhan (SE-2424) — Frontend & Database Developer; Kurmanbayeva Nazym (SE-2413) — Backend & AI Developer

**Status:** Proposed logical design for team and supervisor review  
**Proposed database:** PostgreSQL

## 1 Purpose and scope

The database will support accounts, volunteer profiles, event roles, shifts, applications, organizer decisions, assignments, participation records, task updates, notifications, saved opportunities and matching evaluation. This document is a design specification; it does not claim that database tables or migrations have already been implemented.

The design uses an event-role-shift structure. For example, an event can require registration assistants and photographers, and each role can have morning and afternoon shifts. Each shift has its own time interval, application deadline and capacity. A student applies to a particular role's shift, so the organizer can assess both skills and time availability.

For the initial version, each event has one organizer owner. An organizer can also volunteer for another organizer's event through a volunteer profile. Multiple co-organizers, recurring availability rules, native mobile applications and external university-system integrations are outside this initial design. These boundaries should be checked against user discussions.

## 2 Entity relationship diagrams

The editable Mermaid definitions below render directly in GitHub Markdown. The diagrams are split into related views for readability. The table dictionary in Section 3 defines all seventeen proposed tables, including supporting tables omitted from the diagrams.

**Notation:** PK = primary key; FK = foreign key; UK = unique key. `||` means exactly one, `o|` means zero or one, and `o{` means zero or more. FK denotes an actual relationship to another table, not just a similarly named field.

### 2.1 Accounts and event structure

<img width="400" height="900" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/a0e2472f-3ca6-4196-9f08-08b4881ade9c" />

### 2.2 Applications and participation

<img width="400" height="750" alt="mermaid-diagram (1)" src="https://github.com/user-attachments/assets/ca5d4e91-b209-41b7-85dc-5e2469f4650b" />


An assignment obtains its volunteer, shift, role and event through its application. These identifiers are not copied into the assignment table, avoiding inconsistent duplicate values. `assigned_by`, attendance recorders and task-update authors reference `users`, as specified below.

### 2.3 Matching records

<img width="400" height="650" alt="mermaid-diagram (2)" src="https://github.com/user-attachments/assets/bbbc2cd2-c5e3-4ec7-bed5-fe3729a64ced" />


Skills and interests are connected through the tag tables described below. Availability intervals are stored separately from shifts: a volunteer's availability describes when they can help, while a shift describes when help is needed.

## 3 Table dictionary

Unless indicated otherwise, IDs use `uuid`. Required fields will receive `NOT NULL` constraints in the implementation. Lifecycle records include `created_at` and `updated_at` timestamps unless an exception is stated. Foreign-key references use the form `table.column`. Optional means the field may be null. Status values are controlled values, not arbitrary user text.

### 3.1 Accounts and volunteer attributes

| Table | Main columns and types | Purpose and keys |
|---|---|---|
| `users` | `id uuid`; `full_name text`; `email text`; `password_hash text`; `account_role text`; `is_active boolean`; timestamps | PK: `id`. Unique index on normalized email. Roles: `volunteer`, `organizer`, `administrator`. Passwords are stored as hashes only. Organizer/admin privileges require an authorized grant, not a freely editable registration field. |
| `volunteer_profiles` | `user_id uuid`; `student_group text` (optional); `bio text` (optional); `experience_summary text` (optional); timestamps | PK and FK: `user_id → users.id`. One optional volunteer profile per account, including an organizer account that also volunteers. |
| `tags` | `id uuid`; `kind text`; `name text` | PK: `id`. `kind`: `skill` or `interest`. Unique normalized `(kind, name)`. Shared vocabulary avoids variants such as `Python` and `python` being treated as different skills. |
| `volunteer_tags` | `volunteer_id uuid`; `tag_id uuid` | Composite PK: `(volunteer_id, tag_id)`. FKs to `volunteer_profiles.user_id` and `tags.id`. Many-to-many link for declared skills and interests. Declared skills are not automatically treated as verified qualifications. |
| `availability` | `id uuid`; `volunteer_id uuid`; `starts_at timestamptz`; `ends_at timestamptz`; timestamps | PK: `id`. FK to `volunteer_profiles.user_id`. Stores dated availability intervals; `ends_at > starts_at`. Recurring weekly availability can be added later. |

Using one tag catalog for skills and interests keeps the pilot small while retaining a normalized many-to-many design. The `kind` field distinguishes the two uses. Required certifications, if later needed, should have a separate verification workflow rather than being inferred from free-text experience.

### 3.2 Events and roles

| Table | Main columns and types | Purpose and keys |
|---|---|---|
| `events` | `id uuid`; `organizer_id uuid`; `title text`; `description text`; `category text`; `location text`; `starts_at timestamptz`; `ends_at timestamptz`; `status text`; timestamps | PK: `id`. FK: `organizer_id → users.id`. Status: `draft`, `published`, `completed`, `cancelled`, `archived`. Organizer ownership controls event management. Category values should be agreed with pilot users. |
| `event_roles` | `id uuid`; `event_id uuid`; `title text`; `responsibilities text`; timestamps | PK: `id`. FK: `event_id → events.id`. Defines a role such as photographer or registration assistant. An event can have multiple roles. |
| `role_tags` | `event_role_id uuid`; `tag_id uuid`; `is_required boolean`; `weight numeric` | Composite PK: `(event_role_id, tag_id)`. FKs to `event_roles.id` and `tags.id`. Weight is positive. Only skill tags may be mandatory; interest tags are preferences. This cross-table rule is validated by the service or a trigger. |
| `shifts` | `id uuid`; `event_role_id uuid`; `starts_at timestamptz`; `ends_at timestamptz`; `application_deadline timestamptz`; `capacity integer`; `status text`; timestamps | PK: `id`. FK: `event_role_id → event_roles.id`. Capacity is positive. Status: `open`, `closed`, `cancelled`. Time interval must fall within the event interval; deadline must be no later than shift start. An application is accepted only before the deadline for an open shift in a published event. |

### 3.3 Recruitment and participation

| Table | Main columns and types | Purpose and keys |
|---|---|---|
| `applications` | `id uuid`; `volunteer_id uuid`; `shift_id uuid`; `motivation text` (optional); `status text`; `reviewed_by uuid` (optional); `reviewed_at timestamptz` (optional); `decision_note text` (optional); timestamps | PK: `id`. FKs to volunteer profile, shift and reviewing user. Unique `(volunteer_id, shift_id)` prevents duplicate submissions. Status: `pending`, `accepted`, `rejected`, `withdrawn`. A resubmission, if allowed before the deadline, updates the same record. |
| `assignments` | `id uuid`; `application_id uuid`; `assigned_by uuid`; `status text`; `assigned_at timestamptz`; `updated_at timestamptz` | PK: `id`. Unique FK: `application_id → applications.id`. FK: `assigned_by → users.id`. Status: `assigned`, `confirmed`, `cancelled`. An application creates at most one assignment; reactivation updates that assignment. Both assigned and confirmed records reserve capacity. |
| `attendance` | `assignment_id uuid`; `status text`; `check_in_at timestamptz` (optional); `check_out_at timestamptz` (optional); `recorded_by uuid`; `note text` (optional); timestamps | PK and FK: `assignment_id → assignments.id`. FK: `recorded_by → users.id`. Status: `present`, `absent`, `excused`. No row means not recorded, not absent. Checkout requires check-in and must be later. Worked duration is calculated from valid timestamps; it is not independently edited. |
| `task_updates` | `id uuid`; `assignment_id uuid`; `author_id uuid`; `task_title text`; `details text`; `status text`; `created_at timestamptz` | PK: `id`. FKs to assignment and authoring user. Status: `todo`, `in_progress`, `done`, `blocked`. An append-only update stream records progress on responsibilities within an assignment. This is a simple timeline, not a full project-management subsystem. |

Applications express interest; assignments reserve a place; attendance records what happened. These are different concepts. An accepted application can retain its decision even after an assignment is cancelled. The interface must therefore show assignment cancellation alongside the original accepted decision, rather than implying the student remains scheduled.

### 3.4 Matching and user support

| Table | Main columns and types | Purpose and keys |
|---|---|---|
| `match_runs` | `id uuid`; `shift_id uuid`; `requested_by uuid`; `method_version text`; `parameters jsonb`; `role_snapshot jsonb`; `created_at timestamptz` | PK: `id`. FKs to shift and requesting user. Records the algorithm/configuration and the relevant role requirements and shift times at evaluation time. Each run represents one shift and one method version. |
| `match_results` | `id uuid`; `match_run_id uuid`; `volunteer_id uuid`; `score numeric`; `eligible boolean`; `explanation jsonb`; `profile_snapshot jsonb`; `created_at timestamptz` | PK: `id`. FKs to run and volunteer profile. Unique `(match_run_id, volunteer_id)`. Score between 0 and 1. Snapshots retain only the matching inputs used, such as tags, availability and relevant scheduling conflicts; exclude names, email and passwords. |
| `notifications` | `id uuid`; `recipient_id uuid`; `event_id uuid` (optional); `application_id uuid` (optional); `assignment_id uuid` (optional); `kind text`; `message text`; `read_at timestamptz` (optional); `created_at timestamptz` | PK: `id`. FKs to recipient and the linked resource. Supports in-app messages for application decisions, assignments and schedule changes. If multiple resource links are present, they must describe the same workflow. External email/SMS delivery is separate and is not claimed here. |
| `saved_events` | `user_id uuid`; `event_id uuid`; `created_at timestamptz` | Composite PK: `(user_id, event_id)`. FKs to users and events. Supports saved opportunities without duplicate entries. |

JSONB is limited to evaluation snapshots, method parameters and structured explanation details. Ordinary relationships such as event ownership and applications remain explicit foreign keys. The design does not require a particular AI vendor, external model or vector database.

## 4 Integrity and business rules

### 4.1 Database-enforced constraints

- Every table has a primary key, including composite keys on linking tables.
- Foreign keys prevent applications, assignments and attendance from referencing missing parents.
- Unique constraints prevent duplicate volunteer tags, role tags, saved events, applications for the same shift, assignments for the same application and results for the same volunteer/run.
- Same-row checks require valid status values, positive capacities/weights, valid score ranges, and end times later than start times.
- `reviewed_by` and `reviewed_at` must both be present for accepted/rejected applications. Pending applications have neither. Withdrawn applications may retain a prior review.
- Check-in/out timestamps, when present, are valid only for `present` attendance, and checkout requires an earlier check-in.

Primary keys, foreign keys and checks complement application validation [P1]. Cross-table rules below cannot be expressed as ordinary same-row check constraints alone.

### 4.2 Service rules and transactions

1. **Ownership:** Only the event owner or an authorized administrator may change its roles, shifts, applications or attendance. A matching score does not grant authority.
2. **Application eligibility:** The account and volunteer profile must be active, the event published and the shift open before its deadline. The event owner cannot apply to their own event.
3. **Approval:** Review and assignment creation happen in one transaction. Acceptance requires a place, mandatory skill eligibility and no conflicting active assignment. A missing availability interval is treated as unknown, not proof of availability; request confirmation before assignment.
4. **Capacity and conflicts:** Lock the volunteer's profile row and shift row in a consistent order, recheck active assignments and capacity, then write the approval and assignment. Every capacity-changing operation and assignment path must follow this protocol. Simultaneous approvals must not overbook a shift or double-book a volunteer [P3].
5. **Time overlap:** Intervals use half-open semantics `[start, end)`: a shift ending at 12:00 does not conflict with one starting at 12:00. Availability must cover the entire shift for an automatic availability match.
6. **Cross-table time validation:** A shift must remain inside its event's time interval. Editing an event or shift must revalidate child shifts, existing assignments and volunteer conflicts, not just the edited row.
7. **Schedule changes:** Do not silently move confirmed volunteers. Mark affected active assignments as needing reconfirmation by returning them to `assigned`, notify volunteers and require conflict resolution before finalizing an incompatible schedule.
8. **Withdrawal and cancellation:** A volunteer may withdraw a pending/accepted application before the agreed cutoff. For an accepted application, withdrawal also cancels its active assignment. Event cancellation closes/cancels child shifts, cancels future active assignments and notifies affected volunteers in the same workflow.
9. **Attendance:** Record attendance only for an active assignment and an appropriate shift time, or through an explicitly recorded organizer correction. Cancelled assignments do not receive new attendance records. Historical attendance is preserved.
10. **Task updates:** Volunteers can add updates only to their own assignments; the event owner can update assignments for that event. Author identity comes from the authenticated session.
11. **Matching freshness:** Changed role requirements, tags, availability or assignment conflicts make prior recommendations stale. Recompute before using them for a decision. The server rechecks live eligibility during acceptance regardless of the stored score.

Availability and capacity policy details, including withdrawal cutoff and whether complete availability confirmation is mandatory, should be agreed with actual organizers before implementation.

## 5 Matching data and evaluation

The initial organizer recommendation pool consists of volunteers with **pending applications for the selected shift**. The design does not give organizers unrestricted access to every student profile. Broader proactive recruitment would require a separate opt-in visibility policy.

The matching method can combine skill coverage, interest overlap and availability after checking mandatory constraints. A simple skills-based baseline and a richer candidate method use the same candidate pool. Store separate runs with their method versions and parameters so results can be compared.

For example, an explanation may identify matched skills, missing requirements and whether availability covers the shift. A stored score is a ranking value, not a calibrated probability that a volunteer will perform well. Organizer approval remains separate from algorithm output. Real organizer decisions can inform analysis but should not automatically be treated as unbiased ground-truth labels.

The snapshots make the recorded scores interpretable after profile changes. They contain only the minimum relevant inputs and remain subject to the same access and retention restrictions as profiles. Human relevance labels and the experimental question set can initially remain in a separately versioned evaluation dataset; no extra production tables are necessary for the checkpoint.

## 6 Access and privacy

| Actor | Allowed operations |
|---|---|
| Visitor | Read published event information; no access to candidate profiles or participation records. |
| Volunteer | Edit their profile, tags and availability; manage their own applications and saved events; view their own assignments, attendance and notifications. |
| Organizer | Manage owned events and related recruitment; view relevant applicant matching attributes, make assignments and record attendance. Cannot access other organizers' private applicant records. |
| Administrator | Manage account permissions and perform authorized oversight actions. Administrator access is not available through ordinary self-registration. |

Backend authorization applies on every request, including direct object-ID requests. The browser does not connect to PostgreSQL with administrator credentials. Only a password hash is stored; authentication tokens and password-reset implementation are outside this logical ER model and must be added to the authentication design if persistent token storage is needed.

Use synthetic profiles in a public repository. Do not commit real student data, credentials or database backups. Accounts and events with participation history should normally be deactivated or archived rather than casually deleted. Cascading deletion is appropriate only for disposable dependent records such as unused tag links; historical application, assignment and attendance relationships use restrictive deletion rules. Agree retention and anonymization procedures before collecting pilot data, including snapshots and notifications.

## 7 Time storage and indexes

Store dated instants as `timestamptz`; use `Asia/Qyzylorda` as the proposed display timezone for the AITU pilot. PostgreSQL stores the instant rather than the originally supplied timezone name, so the display timezone is explicit application configuration [P2]. Event/shift deadlines are compared against server time, not the user's device clock.

Initial index candidates, to confirm against actual queries:

| Access pattern | Candidate index or existing key |
|---|---|
| Account lookup | Unique index on normalized email. |
| Published event feed | `events(status, starts_at)`; organizer dashboard: `events(organizer_id, status)`. |
| Event role and shift lookup | `event_roles(event_id)` and `shifts(event_role_id, starts_at)`. |
| Organizer application queue | `applications(shift_id, status)`; volunteer history: `applications(volunteer_id, created_at)`. |
| Profile tags and role requirements | Composite keys on linking tables; reverse indexes beginning with `tag_id` when required. |
| Availability lookup | `availability(volunteer_id, starts_at)`. |
| Matching runs/results | `match_runs(shift_id, created_at)` and `match_results(match_run_id, eligible, score)`; profile-result lookup begins with `volunteer_id`. |
| Notification inbox | `notifications(recipient_id, read_at, created_at)`. |
| Assignment task timeline | `task_updates(assignment_id, created_at)`. |

Primary/unique constraints already create supporting indexes. Check uncovered foreign-key lookup paths, such as reviewer/recorder references, and add indexes where joins, access patterns or parent-update checks justify them. Avoid duplicating indexes with equivalent leading columns. Measure query plans before adding specialized search indexes; full-text or vector search is not required for the initial design.

## 8 Example end-to-end workflow

1. An organizer creates an event, a registration-assistant role and a shift with capacity three.
2. Students maintain profiles, skill/interest tags and availability, then apply to the shift. Applications are `pending`.
3. A matching run evaluates the pending applicants and stores scores, eligibility explanations and input snapshots.
4. The organizer accepts a candidate. One transaction rechecks authorization, eligibility, capacity and time conflicts, sets the application to `accepted` and creates an `assigned` assignment.
5. The volunteer confirms; the assignment becomes `confirmed`. Relevant updates appear in their notification inbox.
6. The organizer records attendance against the assignment. Task updates retain the progress timeline; completed attendance contributes to the volunteer's participation history.

## 9 Verification planned for implementation

- Reject duplicate applications for the same volunteer and shift.
- Reject assignments whose application is not approved or belongs to a different event owner.
- Race two approvals for the final place and verify only one succeeds.
- Race approvals for overlapping shifts for the same volunteer and verify double-booking is prevented.
- Reject invalid event/shift boundaries, negative capacities and reversed attendance times.
- Verify that withdrawing from an accepted application frees the place through assignment cancellation.
- Verify that changing profile data marks prior matching results stale for current use while preserving historical snapshots.
- Verify that unrelated users cannot retrieve profiles, applications, matching snapshots, attendance or notifications through guessed IDs.
- Confirm that completed historical participation remains intact when an event is archived.

These are planned checks, not test results. SQL migrations and executable tests will be added during implementation and kept consistent with this document.

## 10 Technical references

Accessed 20 October 2026. These references support database mechanics; the project's entities and business rules are proposed design decisions.

- **[P1] PostgreSQL — Constraints.** <https://www.postgresql.org/docs/current/ddl-constraints.html>
- **[P2] PostgreSQL — Date/Time Types.** <https://www.postgresql.org/docs/current/datatype-datetime.html>
- **[P3] PostgreSQL — Explicit Locking.** <https://www.postgresql.org/docs/current/explicit-locking.html>
