# Existing System Comparison

**Project:** Development of a Web-Based Volunteer and Event Management System for Astana IT University: Recruitment, Intelligent Matching, and Activity Coordination

**Prepared by:** Aitkali Ayazhan (SE-2424) and Kurmanbayeva Nazym (SE-2413)

## Purpose and method

This comparison examines four existing volunteer-management products against eight criteria derived from the proposed AITU system. The criteria cover discovery, profiles, recruitment, matching, assignment, scheduling and communication, participation records, and reporting. These functions support the planned workflow from a student's application to an organizer's assignment and attendance record.

Evidence comes from official product pages and support documentation. This is a documentation-based comparison, not a hands-on performance or usability test. A documented feature may require a particular subscription, product edition, or configuration. **Not verified** means the reviewed sources did not establish the specific capability; it does not mean the capability is absent. Product features may change after the review date.

The selected products cover organization-level volunteer management and coordination across organizations. Volunteer Impact and Get Connected are compared as separate product offerings, although the Get Connected site states that it is now part of Better Impact [8]. The comparison therefore concerns four products, not four independent vendors.

## Comparison table

| Criterion | Better Impact — Volunteer Impact | VolunteerHub | Rosterfy | Galaxy Digital — Get Connected |
|---|---|---|---|---|
| **1. Opportunity discovery** | Opportunities and volunteer self-registration are documented. The full set of search filters was not verified [1,2]. | Opportunity landing pages and event signups support discovery. Exact search filters were not verified [4]. | Recruitment listings and volunteer access to opportunities are documented. Exact discovery filters were not verified [7]. | Center provides centralized organization and opportunity listings. Public/private opportunities and calendars are documented [8,9]. |
| **2. Volunteer profiles** | Configurable volunteer records and profile availability support administration and scheduling [2,3]. | A volunteer database records contact details, skills and availability; configurable forms collect additional information [4,5]. | Volunteer records support onboarding and qualification management. Matching uses skills, availability and interests; exact profile configuration requires confirmation [6,7]. | Custom profiles display skills, interests, achievements and participation information [9]. |
| **3. Recruitment and applications** | Application and custom intake forms support recruitment and onboarding [1]. | Recruitment tools, registration and configurable forms support signups. Detailed candidate-review states require confirmation [4]. | Recruitment listings, automated onboarding and compliance workflows support recruitment [7]. | Event pages collect volunteer signups; qualifications and prerequisites can inform scheduling. Detailed approval states require confirmation [9]. |
| **4. Volunteer matching** | Availability and assignment tools are documented. An automated ranked suitability recommendation was not verified in the reviewed pages [2]. | Skills/interests groups target recruitment and restrict event eligibility. Automated suitability ranking was not verified [5,10]. | Automated matching using skills, availability and interests is documented. Ranking weights and per-recommendation explanations were not verified [6]. | Center documents automatic skills/interests matching. This claim applies to Center; equivalent functionality across all editions was not verified [8]. |
| **5. Role and responsibility assignment** | One-time/recurring events support role assignments and organizer scheduling [1,2]. | Events, shifts and groups organize placements; group membership can reserve or restrict access to particular opportunities [4,10]. | Role offers and criteria-based shift assignment support staffing across roles and locations [6]. | Organizers schedule volunteers and send shift invitations. Detailed task-progress tracking was not verified [9]. |
| **6. Schedules and notifications** | Shift schedules, self-scheduling and reminders are documented; access varies by subscription plan [2]. | Volunteer scheduling and automated email/text communication support reminders and updates [4]. | Automated scheduling, two-way messaging, email, SMS and app notifications are documented [6]. | Recurring/custom schedules and push reminders are documented; Center also lists automated welcome and reminder messages [8,9]. |
| **7. Attendance and participation records** | Mobile/kiosk check-in and volunteer-hour tracking are documented [1,2]. | Volunteer check-in, hour tracking and activity records are documented [4]. | Desktop/mobile check-in, QR codes, geofencing and shift outcomes are documented [6]. | Self-check-in, kiosk/app options and automated hour tracking are documented [9]. |
| **8. Reporting and analytics** | Reports cover hours, attendance and scheduling; exports by program, date or volunteer type are documented [1,2]. | Standard reports cover volunteer attendance, activity and trends [4]. | Dashboards and reporting cover onboarding, training, attendance and volunteer impact [6,7]. | Hour reporting is documented; Center additionally reports participation across organizations and the value of logged hours [8,9]. |

## Findings and implications for the AITU project

### Functions already available in existing products

The reviewed products already address much of the planned recruitment and coordination workflow. Profiles, signups, scheduling and participation records should therefore be treated as established functional patterns, rather than novel features of the proposed system. Rosterfy and Get Connected Center also document automated matching [6,8]. An absence of matching in competing products would not be a supported justification for this diploma project.

The documented matching capabilities do not establish how well those products would recommend volunteers for AITU event roles. Public feature descriptions also do not provide enough information to reproduce their ranking algorithms or compare their performance under identical conditions. This is a limit of this review, not evidence that the products lack effective or explainable matching.

### Proposed contribution

Our proposed contribution is to design, implement and evaluate a focused AITU workflow: students provide skills, interests and availability; organizers define event-role requirements; the system recommends candidates; organizers approve assignments; and participation is recorded.

We plan to show the factors behind recommendations and evaluate the matching method against a simple skills-based baseline using organizer-reviewed judgments. These are proposed project features and experiments, not demonstrated advantages over commercial products. Native mobile applications and external university-system integrations remain outside the initial scope.

### University context and justification

A university audience alone does not establish a market gap. Get Connected offers a Campus product for student volunteerism and service learning, while Rosterfy explicitly lists universities and colleges among its audiences [7,11]. The project must therefore justify its scope through actual AITU discussions and a comparison of implementation versus adopting or configuring an existing service.

The university should identify which application-review steps, role requirements, availability constraints, assignment decisions and attendance records matter locally. Three to five discussions with representative students and organizers will inform that decision. The comparison does not establish that commercial products are unsuitable, unaffordable or unavailable to AITU.

## Limits and follow-up verification

- Exact discovery filters, detailed application-status workflows and matching explanations should be checked in demonstrations or trials where available.
- Confirm subscription and edition boundaries before treating a feature as included; scheduling restrictions are explicitly documented for Volunteer Impact [2].
- Separate ordinary qualification or group filtering from automated ranking when evaluating intelligent matching.
- Test the same small set of role descriptions and candidate profiles when comparing accessible matching implementations.
- Record the actual feature configuration, review date and observed results. Do not convert unverified capabilities into negative scores.

## Official sources

All sources below were accessed on **20 October 2026**. Reference numbers in the table identify the pages supporting each entry.

1. **Better Impact — Volunteer Management Software.** Recruitment forms, role assignments, check-in, communication and reports. <https://www.betterimpact.com/volunteer-management-software>
2. **Better Impact — Volunteer Scheduling Software Features.** Schedules, availability, assignments, reminders, reporting and plan restrictions. <https://www.betterimpact.com/how-we-help/volunteer-scheduling-software-features>
3. **Better Impact — Volunteer Database Software Features.** Volunteer records and database administration. <https://www.betterimpact.com/how-we-help/volunteer-database-features>
4. **VolunteerHub — Volunteer Management Software for Nonprofits.** Recruitment, forms, scheduling, communication, check-in and reporting. <https://volunteerhub.com/platform>
5. **VolunteerHub — Volunteer Recruitment, Scheduling and Management Platform.** Volunteer database, skills and availability. <https://volunteerhub.com/>
6. **Rosterfy — Advanced Scheduling.** Skills/availability/interests matching, assignments, communications, attendance and dashboards. <https://www.rosterfy.com/platform/advanced-scheduling/>
7. **Rosterfy — Volunteer Management Software.** Recruitment, onboarding, reporting and university audience. <https://www.rosterfy.com/>
8. **Galaxy Digital — Get Connected Center.** Centralized opportunity discovery, automatic matching, reminders, reports and product-family notice. <https://www.galaxydigital.com/products/nonprofit-engagement/center>
9. **Galaxy Digital — Volunteer Scheduling Software.** Profiles, prerequisites, invitations, calendars, notifications and participation tracking. <https://www.galaxydigital.com/features/volunteer-scheduling-software/>
10. **VolunteerHub — Volunteer Group Management and Organization.** Skill/interest groups, eligibility restrictions and targeted communication. <https://volunteerhub.com/platform/group-organization>
11. **Galaxy Digital — Get Connected Product Suite.** Campus offering and differences between products. <https://www.galaxydigital.com/products>


