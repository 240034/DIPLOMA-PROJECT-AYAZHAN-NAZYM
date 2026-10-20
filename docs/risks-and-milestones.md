# Risks and Milestones

**Project:** Development of a Web-Based Volunteer and Event Management System for Astana IT University: Recruitment, Intelligent Matching, and Activity Coordination

**Team:** Aitkali Ayazhan (SE-2424) — Frontend & Database Developer; Kurmanbayeva Nazym (SE-2413) — Backend & AI Developer

**Prepared:** 20 October 2026  
**Status:** Proposed risk register and schedule; milestone completion must be recorded from actual evidence.

## 1 Planning assumptions

The project is developed by two students using HTML, CSS and JavaScript for the frontend, Python with FastAPI for the backend, and PostgreSQL for storage. The initial scope covers profiles, events and volunteer shifts, applications, recommendations, organizer assignments, schedules, task updates, notifications and attendance.

Matching supports organizer decisions; recommendations do not automatically accept or assign volunteers. Native mobile applications and external university-system integrations are outside the initial scope. Initial notifications can be delivered inside the website, without depending on an external email or SMS provider.

The 24 October checkpoint concerns analysis, design, planning and review. The schedule below does not assume a complete application is required by that date. Later implementation deadlines must be agreed with the supervisor.

## 2 Risk assessment method

Likelihood and impact are estimated on a three-point scale: **1 = low, 2 = medium, 3 = high**. Priority is likelihood multiplied by impact: **1–2 low, 3–4 medium, 6–9 high**. These are initial planning judgments, not measured probabilities.

Each risk has a lead owner, a warning sign, preventive actions and a fallback response. The owner coordinates the response; both members remain responsible for integration and review.

## 3 Risk register

| ID | Risk and consequence | Likelihood | Impact | Priority | Warning sign | Prevention and fallback | Lead owner |
|---|---|---|---|---|---|---|---|
| R01 | **Insufficient user evidence.** Features may not address actual AITU recruitment or coordination difficulties. | 2 | 3 | 6 — High | Student/organizer discussions are not arranged, or important decisions rely only on assumptions. | Arrange 3–5 representative discussions and link findings to requirements. If access is delayed, narrow the pilot and retain explicit assumptions; do not invent findings or claim validated demand. | Nazym |
| R02 | **Scope growth.** Extra functions delay the mandatory workflows. | 3 | 3 | 9 — High | New features are added without changing the schedule or removing other work. | Freeze a minimum scope and record priorities. Postpone external integrations, native mobile support and additional AI functions before cutting core recruitment and assignment work. | Nazym |
| R03 | **Frontend/backend mismatch.** Different field names, status values or response formats break integration. | 2 | 3 | 6 — High | The UI and API use different application states or incompatible data structures. | Agree example requests/responses and status definitions before parallel implementation. Integrate one complete flow early; resolve contract differences before building more screens. | Ayazhan |
| R04 | **Weak matching results or too little evaluation data.** Recommendations may be unsuitable or their value cannot be demonstrated. | 2 | 3 | 6 — High | Candidate rankings conflict with required skills or lack organizer-reviewed evaluation examples. | Establish a skills-based baseline and obtain representative reviewed cases. Evaluate richer scoring against the same baseline and candidates. If it does not improve results, report the finding and retain the simpler method; do not claim an unmeasured AI benefit. | Nazym |
| R05 | **Overbooking or conflicting assignments.** Simultaneous approvals can exceed shift capacity or assign one volunteer to overlapping shifts. | 2 | 3 | 6 — High | Two concurrent approvals obtain the final place, or an overlap appears in a volunteer's schedule. | Coordinate acceptance and assignment in transactions, with capacity and conflict checks. Test concurrent approvals. If a conflict occurs, stop further approvals for the affected shift, correct assignments with the organizer and notify volunteers. | Nazym |
| R06 | **Unauthorized access to student information.** Users may view or change another person's applications, profile data or participation records. | 2 | 3 | 6 — High | A request using another user's resource ID succeeds, or an organizer can access another organizer's private applicant records. | Enforce ownership and permissions on the backend, not only in the UI. Test negative-access cases and use synthetic data during development. If a check fails, block the affected feature and fix it before real-user testing. | Nazym |
| R07 | **Schema drift or data loss.** Uncoordinated database changes break the API, duplicate records or damage participation history. | 2 | 3 | 6 — High | Manual table edits differ between environments, or migrations fail on a shared test database. | Version migrations and review schema changes together. Back up pilot data before risky changes and check restoration. If a change fails, restore the last validated state and correct the migration before continuing. | Ayazhan |
| R08 | **Confusing interface.** Users cannot find shifts, understand application status or complete organizer tasks. | 2 | 2 | 4 — Medium | Prototype participants hesitate, need help or confuse applying with confirmed participation. | Test the core Figma flows with students and organizers. Use clear status labels and feedback. Revise failed task flows before adding visual detail or optional screens. | Ayazhan |
| R09 | **Late review or missing submission evidence.** Incomplete links, unsupported decisions or missing feedback weaken the checkpoint submission. | 2 | 3 | 6 — High | Documents remain unlinked, the prototype cannot be opened, or supervisor review has not been arranged before 23 October. | Maintain a checklist, request substantive review early and test access from a reviewer account. Correct broken links, record actual outstanding items and avoid marking unreviewed work complete. | Nazym |
| R10 | **Uneven workload or one member becoming unavailable.** Work depends on knowledge held by only one person. | 2 | 2 | 4 — Medium | One member has several blocked tasks, or the other cannot explain or run their part. | Assign bounded tasks, review each other's changes and document setup/contracts. Reassign urgent work where feasible and reduce optional scope if availability changes. | Ayazhan |

## 4 Milestones for the 24 October checkpoint

Dates are proposed work targets. A milestone is complete only when its stated evidence is available; the table does not claim these tasks have already been finished.

| ID | Target date | Milestone | Completion evidence | Lead and review |
|---|---|---|---|---|
| M01 | 20 October | Consolidate scope and repository documentation. | One current project description; README lists the stack, responsibilities, supervisor, expected outcomes and truthful status; duplicate comparison files are resolved. | Nazym leads; Ayazhan reviews. |
| M02 | 21–22 October | Collect and analyze local user evidence. | 3–5 documented discussions with representative volunteers/organizers, or the required substantive client agreement; findings are distinguished from assumptions and linked to requirements. | Nazym coordinates; both participate. |
| M03 | 21–22 October | Complete requirements and the evaluation plan. | Prioritized functional/non-functional requirements, acceptance criteria, proposed metrics, measurement conditions and a matching baseline. | Nazym leads; Ayazhan reviews. |
| M04 | 22 October | Align prototype, architecture and database design. | Core volunteer and organizer prototype flows; context, use case and draft component diagrams with editable sources and readable exports; data design uses consistent entities and statuses. | Ayazhan leads prototype/data review; Nazym checks backend/matching consistency. |
| M05 | 22–23 October | Finalize research and technology justification. | Literature synthesis and publication table with at least 12 meaningfully used sources, including 8 scientific publications; existing-system comparison and three technology decisions with alternatives and reasons. | Both review; Nazym coordinates. |
| M06 | 23 October | Obtain supervisor feedback and apply revisions. | Dated comments on key deliverables, recorded team responses and links to actual revisions. A request for feedback alone does not complete this milestone. | Both members. |
| M07 | By 24 October | Prepare the reviewed checkpoint submission. | Accessible repository and prototype; required documentation linked; assigned/prioritized tasks; contribution and review history from both members; submission tag, completed-work summary, limitations and outstanding tasks. | Both members. |

If review or user access is delayed, record that limitation and revise the schedule with the supervisor. A missed evidence requirement remains outstanding rather than becoming complete through a placeholder document.

## 5 Implementation milestones after the checkpoint

Exact dates will be agreed after the 24 October review. The sequence below identifies dependencies without inventing a final-defense deadline.

| Stage | Planned result | Completion criterion | Main dependency |
|---|---|---|---|
| I01 — Foundation | Accounts, permissions, schema and a connected UI/API. | An authorized organizer creates an event and shift; the browser displays saved data. Unauthorized changes are rejected. | Agreed requirements, API contract and initial migrations. |
| I02 — Recruitment | Profiles, availability, applications and status tracking. | A student applies once to a shift; the organizer reviews it; duplicate and unauthorized operations fail. | I01 and role/shift validation. |
| I03 — Assignment and coordination | Assignment confirmation, schedules, task updates and in-app notifications. | Approval reserves capacity; conflicts are blocked; cancellation updates the schedule and relevant users are notified. | I02 and tested assignment transactions. |
| I04 — Matching | Baseline and candidate ranking method with explanations. | Both methods run on the same reviewed cases; method versions and results are retained; organizer approval remains separate. | Suitable profiles/roles, evaluation cases and agreed metrics. |
| I05 — Participation | Attendance and participation history. | The event owner records participation against valid assignments and history remains consistent. | I03 and agreed attendance rules. |
| I06 — Evaluation and refinement | Functional, integration, usability and matching evaluation. | Actual results, failures and limitations are recorded; critical permission/assignment defects are resolved before pilot release. | Core workflows, available participants and frozen evaluation cases. |

The interface may be developed with sample data in parallel, but a screen is not considered integrated until it has been checked against the actual API.

## 6 Dependencies and decisions to confirm

| Dependency | Why it matters | Required action |
|---|---|---|
| AITU volunteers and organizers | Provide evidence for requirements, prototype feedback and matching relevance judgments. | Arrange discussions and agree a limited pilot contact group. |
| Supervisor availability | Scope, evaluation targets and deliverables need substantive review. | Arrange a review before the checkpoint and retain comments and responses. |
| Consistent data and API contracts | Frontend, backend and matching must agree on fields and statuses. | Review contracts together and record changes with the related task. |
| Agreed matching cases | Without relevant examples, matching performance cannot be established. | Obtain reviewed cases; keep development and final evaluation cases separate. |
| Repository and prototype access | The committee needs to inspect the submission. | Check access to the repository, Figma and linked documents before submission. |
| Task-management requirement | The curator names YouTrack, while the current README links ClickUp. | Use YouTrack unless the curator has explicitly accepted ClickUp; record any accepted substitution. |

## 7 Monitoring and completion rules

Before the checkpoint, review blocked tasks and high-priority risks briefly each day. During implementation, review the register weekly and when scope or dependencies change. Link risks to relevant project tasks and update the owner, warning signs and response when needed.

A task is complete only when its acceptance criteria are met, the deliverable is available, and the other member has reviewed relevant changes. Documentation and design work should also appear progressively in repository history. Initial risk ratings are not permanent: reassess them after interviews, prototype feedback, integration checks and evaluation.

High-priority technical failures require action before real-user release. An unresolved issue should have a recorded limitation or blocked task, a responsible person and a next step; it must not be described as a successful test or completed feature.
