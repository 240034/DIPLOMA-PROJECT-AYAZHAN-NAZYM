**Title:** 
Development of a Web-Based Volunteer and Event Management System for Astana IT University: Recruitment, Intelligent Matching, and Activity Coordination

**Members:** 
Aitkali Ayazhan (SE-2424) - [Frontend & Database developer]
Kurmanbayeva Nazym (SE-2413) - [Backend & AI developer]

**Supervisor:**
Nadirov Nurtas - Senior Lecturer

**Brief Description:** 
This diploma project aims to develop a web-based system for volunteer recruitment, intelligent matching, and event activity coordination at Astana IT University.
The proposed system will allow students to discover volunteering opportunities and apply for event roles. Organizers will be able to manage recruitment, review volunteer recommendations, assign responsibilities, and track participation.

**Problem Statement:**
Volunteer recruitment and event coordination require organizers to manage applications, assess candidates, communicate assignments, and monitor participation.
This project investigates how these processes are currently handled at Astana IT University and which difficulties a centralized platform could address. Initial assumptions about user needs will be validated through discussions with student volunteers and event organizers.

**Target Users:**
- Student volunteers: Create profiles, find opportunities, apply for roles, and view assignments and schedules.
- Event organizers: Publish events, recruit volunteers, review recommendations, coordinate activities, and record attendance.
- Administrators: Manage access and oversee platform activity.

**Expected outcomes:**

- A web application for volunteer recruitment and event coordination at Astana IT University.
- Volunteer profiles containing skills, interests, experience, and availability.
- Tools for publishing events, defining volunteer roles and shifts, and reviewing applications.
- Volunteer recommendations based on role requirements and profile information, with organizer approval of assignments.
- Schedules, task updates, in-app notifications, and attendance records.
- Project documentation covering research, requirements, architecture, database design, and evaluation.
- An evaluation report describing functionality, usability, matching performance, and limitations.

**Planned Scope:**
- User authentication and role-based access.
- Volunteer profiles with skills, interests, and availability.
- Event creation and volunteer role descriptions.
- Volunteer applications and application status tracking.
- Recommendations based on role requirements and volunteer profiles.
- Organizer approval and assignment of volunteers.
- Schedules, task updates, and notifications.
- Attendance and participation records.
A native mobile application and external university system integrations are outside the initial scope.


**Current Development Status:**

**Selected technologies:**

| Component | Selected technology | Main reason |
|---|---|---|
| Frontend | HTML, CSS and JavaScript without a frontend framework | Uses technologies already studied by the team and supports the planned forms, lists, dashboards and interactive actions. |
| Backend | Python with FastAPI | Fits the planned API-based application and allows matching logic to remain in Python. |
| Database | PostgreSQL | Fits the relational data model and builds on the team's more recent university experience with PostgreSQL. |


**Project Documentation:**

- **Clickup project:** [(https://app.clickup.com/1100310000028125/v/b/z8q7hb3jex-398)]
- **Figma prototype:** []


| Document | Link |
|----------|------|
| Project proposal and scope | [README.md] |
| User discussions and findings | [Add repository link] |
| Literature review | [https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/blob/main/docs/Source.docx] |
| Existing system comparison | [https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/blob/main/docs/existing-system-comparison.md] |
| Technology comparison |[https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/blob/main/docs/technology-comparison.md] |
| Requirements and acceptance criteria | [https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/blob/main/docs/Acceptance%20Criteria.pdf] |
| Architecture and editable diagram sources | [https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/tree/main/diagrams] |
| Database design | [https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/blob/main/docs/database-design.md] |
| UX prototype | [no link for now] |
| Verification and evaluation plan | [Add repository link] |
| Risks and milestones | [https://github.com/240034/DIPLOMA-PROJECT-AYAZHAN-NAZYM/blob/main/docs/risks-and-milestones.md] |
| Supervisor feedback and revisions | [no link for now] |

**Setup and Execution:**

1. Install the required software and project dependencies.
2. Create a local configuration file from `.env.example`.
3. Configure PostgreSQL and apply database migrations.
4. Start the FastAPI backend and serve the frontend.
5. Run automated tests.



