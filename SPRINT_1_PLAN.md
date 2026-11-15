# Sprint 1 Plan
 
## Project and team
 
- **Project title:** Smart Study Planner
- **Group:** D
- **Team members:**
  - Loulwah Alsahali
  - Malak Alenezi
  - Rifal Meshari Alkhudhair
- **GitHub repository URL:** https://github.com/Loulwah-M/Smart-Study-Planner
- **GitHub Project URL:** https://github.com/users/Loulwah-M/projects/1
- **Sprint dates:** 15 November 2026 – 28 November 2026
- **Sprint length:** Two weeks
## Connection to Assignment 1
 
The project backlog is derived from [`PROJECT_PROPOSAL.md`](PROJECT_PROPOSAL.md). Its 12 issues cover the three proposed workflows:
 
| Workflow | Goal |
|---|---|
| **W1** – Set up my semester | Log in, select courses, enter assignments and exams, and view deadlines |
| **W2** – Generate and follow a weekly study plan | Enter availability, generate study sessions, and track progress |
| **W3** – Respond to a reminder and keep the plan up to date | Receive reminders and update the plan after task changes |
 
The backlog covers all eight functional requirements, FR-01 to FR-08, and the three non-functional requirements: security and privacy (NFR-02) through the access-control test plan, usability and accessibility (NFR-03) through the evaluation issue, and performance (NFR-01) through the acceptance criteria of the dashboard, scheduling and reminder issues.
 
Each issue defines a required outcome, acceptance criteria, and a source reference to the relevant workflow, requirement, or risk in Assignment 1. All issues were added to the GitHub Project with `Status = Backlog`.
 
Sprint 1 selects four requirements and design issues. They establish clear, testable behavior before implementation. The remaining eight issues cover authentication, course selection, task management, the dashboard, scheduling, progress tracking, reminders and automatic updates, and usability and accessibility evaluation.
 
Microsoft Teams integration remains an optional, time-boxed investigation. The core workflows use manually entered data and do not depend on Teams access.
 
## Sprint goal
 
> Produce reviewed, testable specifications for the three core workflows and a simulated data model with an authorization test plan, providing a consistent foundation for the initial prototype.
 
## Selected issues
 
| Issue | Assignment 1 source | Owner | Expected outcome |
|---|---|---|---|
| [#2: Define and review semester setup requirements](https://github.com/Loulwah-M/Smart-Study-Planner/issues/2) | W1; FR-01, FR-02, FR-03, FR-04 | Loulwah Alsahali | Reviewed semester setup specification and acceptance scenarios. Planned evidence: `docs/requirements/W1_SETUP.md`. |
| [#3: Define and review weekly scheduling rules](https://github.com/Loulwah-M/Smart-Study-Planner/issues/3) | W2; FR-05, FR-06; requirements-change risk | Malak Alenezi | Reviewed scheduling rules, progress definitions, and worked examples. Planned evidence: `docs/requirements/W2_SCHEDULING.md`. |
| [#4: Define and review reminders and automatic plan updates](https://github.com/Loulwah-M/Smart-Study-Planner/issues/4) | W3; FR-07, FR-08; requirements-change and external-service risks | Rifal Meshari Alkhudhair | Reviewed reminder and automatic-update rules with acceptance scenarios. Planned evidence: `docs/requirements/W3_UPDATES.md`. |
| [#5: Design the simulated data model and access-control test plan](https://github.com/Loulwah-M/Smart-Study-Planner/issues/5) | W1-W3; FR-01, FR-02, FR-03, FR-05, FR-07, FR-08; NFR-02; privacy/security risk | Rifal Meshari Alkhudhair | Reviewed data model, fictional test data, and at least 15 authorization test cases. Planned evidence: `docs/design/DATA_AND_SECURITY.md`. |
 
### Selection justification
 
These four issues support one sprint goal and suit a two-week planning and specification sprint. Their outputs are bounded documents, scenarios, and test plans rather than a completed application. Each can begin from the Assignment 1 proposal and can be reviewed against the acceptance criteria in its repository issue.
 
The team will resolve unclear behavior, including reminder handling for completed and cancelled tasks, course-progress calculations, and administrator catalogue maintenance. Agreed changes will be recorded consistently in the affected specifications and in the proposal.
 
### Sprint configuration
 
At plan submission:
 
- Only these four issues have `Sprint = Sprint 1`.
- Their status is `Ready`.
- Each issue has its named primary owner assigned through their GitHub account.
- All four appear in the `Current Sprint` board view.
- The other eight issues remain in `Backlog`, with no sprint assigned.
The Project uses an iteration field named `Sprint`, containing a two-week iteration named `Sprint 1`. The `Current Sprint` view is filtered to Sprint 1 and grouped by Status.
 
## Workflow rules
 
- Maximum issues In Progress at one time: 2 across the team.
- **Backlog:** identified project work that has not yet been selected and prepared for the sprint.
- **Ready:** the issue has a clear outcome, acceptance criteria, source reference, assigned owner, and enough information to begin.
- **In Progress:** the owner has started the work, and the team's limit allows it.
- **Review:** the owner has linked the proposed evidence, and another team member checks it against the acceptance criteria.
- **Done:** all acceptance criteria are met, review comments are resolved, and the reviewed evidence is available in the repository.
- Work must be reviewed by a member other than its primary owner before moving to Done.
- Completed issues must link to repository evidence, such as a merged document or pull request.
- Blocked work remains In Progress and counts toward the limit. The owner records the blocker so the team can help resolve it.
- Unfinished or unreviewed work must not be marked Done.
- Each member records their own genuine contributions through issues, commits, pull requests, or reviews.
## Contribution plan
 
| Team member | Work to lead | Work to review | Planned contribution evidence |
|---|---|---|---|
| Loulwah Alsahali | Semester setup specification; coordination of the sprint plan and board | Reminder and automatic-update specification | Issue updates, specification commits or pull requests, and review comments |
| Malak Alenezi | Weekly scheduling specification, worked examples, and progress rules | Semester setup specification; data model and access-control test plan | Issue updates, scheduling examples, specification commits or pull requests, and review comments |
| Rifal Meshari Alkhudhair | Reminder and update specification; simulated data model and authorization test plan | Weekly scheduling specification | Issue updates, design and test-plan commits or pull requests, and review comments |
 
These responsibilities identify primary owners and reviewers. All members will discuss decisions and resolve inconsistencies across the three workflows.
 
### Sprint timeline
 
- **Week 1:** Begin the semester setup and scheduling specifications. Prepare the reminder and data-model work from the proposal, starting additional issues only when an In Progress slot becomes available. Identify unclear requirements and record proposed decisions in the relevant issues.
- **Week 2:** Complete the remaining specifications and the data and security design. Review each output, resolve comments, check consistency across the workflows, and merge accepted documents. Record unfinished work accurately and discuss it during the sprint review.
The team will hold a short weekly coordination meeting and an end-of-sprint review against the sprint goal and the issue acceptance criteria.
 
## AI use disclosure
 
The team used ChatGPT (OpenAI) and Claude (Anthropic) to help draft and organize the backlog, the acceptance criteria, and this sprint plan, using the Assignment 1 proposal and the Assignment 2 instructions. The team is responsible for checking and revising the submitted content. This plan does not claim that implementation, user testing, or peer reviews have already been completed.
