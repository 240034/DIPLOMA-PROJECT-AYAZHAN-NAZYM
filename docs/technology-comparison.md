# Technology Comparison

**Project:** Development of a Web-Based Volunteer and Event Management System for Astana IT University: Recruitment, Intelligent Matching, and Activity Coordination

**Team:** Aitkali Ayazhan (SE-2424) — Frontend & Database Developer; Kurmanbayeva Nazym (SE-2413) — Backend & AI Developer

**Date:** 20 October 2026

## Purpose and selection criteria

This document compares alternatives for three key technical decisions: frontend development, backend development and database management. The choices consider the planned functionality, the two-person team's existing university experience, development time and maintainability. Official documentation supports the feature descriptions; the selection rationale reflects our project requirements and team constraints.

The comparisons are qualitative. We have not conducted performance benchmarks, and the selected technologies are not claimed to be universally better than the alternatives. Implementation and evaluation are planned work.

## Selected technologies

| Component | Selected technology | Main reason |
|---|---|---|
| Frontend | HTML, CSS and JavaScript without a frontend framework | Uses technologies already studied by the team and supports the planned forms, lists, dashboards and interactive actions. |
| Backend | Python with FastAPI | Fits the planned API-based application and allows matching logic to remain in Python. |
| Database | PostgreSQL | Fits the relational data model and builds on the team's more recent university experience with PostgreSQL. |

## 1 Frontend comparison

The interface needs registration and login forms, volunteer profiles, event discovery, application tracking, organizer dashboards and attendance controls.

React also uses HTML-like markup, CSS and JavaScript; the decision is whether to add a component library and its application patterns, rather than whether to replace all three core web technologies.

| Criterion | HTML, CSS and JavaScript | React |
|---|---|---|
| Interface structure | HTML defines content, CSS controls layout and appearance, and JavaScript handles interaction [1]. | Interfaces are assembled from reusable components; state and event handling control interactive behavior [2]. |
| Team experience | The team has studied these technologies and can build on that experience. | The team has not studied React and would need additional learning time. |
| Project suitability | Can implement the planned screens and communicate with backend APIs. DOM updates and shared interface behavior must be organized explicitly. | Component reuse and state management can help coordinate repeated or interdependent interface elements [2]. |
| Main trade-off | Fewer new framework concepts, but greater responsibility for keeping rendering and state handling consistent. | Additional concepts to learn before the team can use the library effectively. |

**Decision:** We will use HTML, CSS and JavaScript without React for the initial implementation. This choice lets us focus on the required volunteer and organizer workflows using familiar technologies. We will organize JavaScript into modules and share styles and rendering functions to reduce duplication. React remains a reasonable alternative, but learning it is not necessary to meet the current scope.

## 2 Backend comparison

The backend must enforce permissions, manage events and applications, approve assignments, record participation and provide matching recommendations. We compare FastAPI and Django, both Python-based alternatives.

| Criterion | FastAPI | Django |
|---|---|---|
| Development approach | API-focused framework with request validation and OpenAPI-based documentation [3]. | Framework with integrated facilities for database models, authentication and administration [4]. |
| Fit with the frontend | Provides endpoints for a separate JavaScript interface to call. | Can serve rendered pages or support an API layer, depending on the selected architecture. |
| Matching logic | Python functions for scoring and recommendations can be called from application services. | Python matching functions can also be integrated; this capability is not exclusive to FastAPI. |
| Team learning and implementation work | Follows our chosen Python/FastAPI direction, but requires explicit selection and implementation of authentication, database access and migrations. | Offers useful integrated tools, but the team has no current Django experience and would need to learn its conventions. |

**Decision:** We will use Python with FastAPI. Its API-focused approach fits the planned JavaScript frontend and keeps recruitment services and matching logic in the same language. Request validation and generated API documentation can help the two developers agree on integration contracts [3]. We will implement authorization and assignment rules explicitly; choosing FastAPI does not provide those business rules automatically.

Django is a valid alternative, particularly when built-in administration and authentication are priorities [4]. Our selection is based on the intended architecture and team familiarity, not a claim that Django is technically inferior.

## 3 Database comparison

The application contains related records: users, volunteer profiles, events, roles, shifts, applications, assignments and attendance. Both PostgreSQL and MySQL are reasonable relational database systems. SQL is the language used to work with these systems, not the name of the database product.

| Criterion | PostgreSQL | MySQL with InnoDB |
|---|---|---|
| Relational integrity | Supports primary keys, foreign keys, unique constraints and checks for enforcing data rules [5]. | Supports primary keys and foreign-key relationships; InnoDB provides transactional storage [6,7]. |
| Suitability for the application | Can represent the proposed event-role-shift relationships and prevent duplicate applications using constraints. | Can also represent these relationships and support the recruitment workflow. |
| Consistent updates | Transactions and appropriate locking can coordinate acceptance, capacity checks and assignment creation [8]. | InnoDB supports transactions and locking for coordinated changes [7]. Correct application logic is required in either database. |
| Team experience | Studied more recently by the team, providing a stronger starting point for implementation. | Studied earlier at university, but is less recent in the team's experience. |

**Decision:** We will use PostgreSQL. Its relational constraints fit the proposed database design, and the team's more recent experience should reduce the amount of relearning needed. For example, a unique volunteer/shift relationship prevents duplicate applications, while an approval transaction can coordinate the application decision and assignment creation.

We do not select PostgreSQL merely because it is described as “more advanced.” MySQL can also meet the core storage requirements. PostgreSQL is selected because it fits our existing design and current team experience. We will verify database correctness through tests for duplicate applications, capacity limits, conflicting assignments and access restrictions.

## 4 How the selected technologies work together

The browser displays HTML pages styled with CSS. JavaScript sends HTTP requests to FastAPI and processes responses, using the Fetch API where appropriate [9]. FastAPI authenticates the request, checks permissions, executes business rules or matching logic, and reads or writes PostgreSQL through a server-side database layer.

Database credentials remain on the server. The frontend communicates with the backend rather than connecting directly to PostgreSQL. Detailed database-access libraries, migration tools, authentication mechanisms and deployment settings will be recorded as they are selected during implementation.

## 5 Official references

Accessed 20 October 2026.

1. **MDN — Core learning modules.** HTML, CSS and JavaScript fundamentals. <https://developer.mozilla.org/en-US/docs/Learn_web_development/Core>
2. **React — Quick Start.** Components, events and state. <https://react.dev/learn>
3. **FastAPI — Features.** Validation and API documentation. <https://fastapi.tiangolo.com/features/>
4. **Django — Overview.** Models, authentication and administration. <https://www.djangoproject.com/start/overview/>
5. **PostgreSQL — Constraints.** <https://www.postgresql.org/docs/current/ddl-constraints.html>
6. **MySQL — Foreign Key Constraints.** <https://dev.mysql.com/doc/refman/8.4/en/create-table-foreign-keys.html>
7. **MySQL — Introduction to InnoDB.** <https://dev.mysql.com/doc/refman/8.4/en/innodb-introduction.html>
8. **PostgreSQL — Explicit Locking.** <https://www.postgresql.org/docs/current/explicit-locking.html>
9. **MDN — Using the Fetch API.** <https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch>
