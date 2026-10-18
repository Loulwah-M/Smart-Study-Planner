# SWE301 Assignment 1: Project Proposal and Initial Requirements
 
## 4.1 Team information
 
**Project title:** Smart Study Planner
 
**Group letter:** D
 
**Team members:**
- Loulwah Alsahali
- Malak Alenezi
- Rifal Meshari Alkhudhair
**GitHub repository URL:** https://github.com/[organisation-or-user]/[repository-name]
 
**summary:** Smart Study Planner is a web application that gathers a university student's courses, assignments, exams and deadlines in one place and turns them into a realistic weekly study schedule.
 
---
 
## 2. Problem and users
 
University students often manage several courses, assignments, exams and study deadlines at the same time, and organising them manually makes it hard to prioritise tasks, distribute study time and remember upcoming deadlines. At our university, a student usually follows five or six courses, and the information about what is due is spread across many places: the PDF or Word syllabus, assignment posts on the learning platform or Microsoft Teams, announcements made in class, messages in group chats, and the student's own notes or phone calendar. When an instructor changes a due date, the change is usually announced in only one of these places, so a student who misses that announcement keeps working towards the old date. Nobody sees all deadlines together, so heavy weeks, where several assignments, quizzes and a project fall close together, are noticed only a few days before they arrive. Students also rarely estimate the hours a task needs, which leads to last-minute work and late submissions.
 
The people who experience this problem are mainly undergraduate students, especially those in their first and second years who have not yet built a personal planning system. Instructors are affected indirectly: they repeat reminders and answer "when is this due?" questions. They will not use the system, so students enter their own dates from the syllabus and announcements. The problem matters because missed or rushed work lowers grades, increases stress, and takes teaching time away from learning. A planner built around the academic calendar, rather than around generic to-do lists, may help reduce these errors.
 
The system has two actors. The **Student** is the primary actor: they add courses, record assignments and exams, view deadlines, receive reminders before upcoming assignments and exams, and generate and follow a study schedule. The **Administrator** manages user accounts and the course catalogue (course code, title, semester and instructor) and loads the simulated demonstration data. Instructors do not log in to the system. Microsoft Teams is not an actor in the first prototype. It is an external service whose integration will be investigated (see Sections 5 and 8).
 
---
 
## 3. Existing solutions
 
Several existing tools help students organise tasks, manage deadlines and plan their schedules, but a student still has to decide how to distribute study time across several courses. We reviewed the current process and four tools to find features that Smart Study Planner can build on and limitations that it aims to address.
 
| Existing process or solution | Useful features | Limitation for our users | Source |
|---|---|---|---|
| **Current process** (syllabi, learning platform/Teams posts, chats, personal notes) | Free, no new tool to learn; the syllabus is the official source of dates | Deadlines are scattered and can be out of date; no combined view; no workload estimate; no warning about heavy weeks | Research on planning and time management: [Patzak et al. (2025)](https://doi.org/10.3389/feduc.2025.1623228) and [Oreopoulos et al. (2022)](https://doi.org/10.3368/jhr.57.1.0919-10426R1). Team observation: our own experience as university students, where deadlines are shared through course syllabi, learning-platform or Teams posts, class announcements and group chats. |
| **Google Calendar** (calendar with tasks) | Tasks with a start date and time, a planned duration and a separate deadline; tasks with dates appear on the calendar; notifications at the task time or on the deadline day; repeating tasks; tasks can be marked complete | The student decides when to study and places study time on the calendar manually. The documentation we reviewed does not describe generating a study plan from deadlines and estimated study hours, or a structure for courses, assignment weight and exams. Smart Study Planner generates the weekly schedule from deadlines, estimated hours and the student's availability | [Google Calendar Help: Create and manage tasks](https://support.google.com/calendar/answer/6285327) |
| **Todoist** (task manager) | Due dates (including natural-language entry), priorities, reminders, projects with sub-tasks and sections, list, board and calendar views, recurring tasks, sync across devices | A general-purpose task manager: the student must still fit tasks into the time available, and the listing we reviewed does not describe academic structures such as courses and exams or automatic study scheduling. Smart Study Planner is built around academic deadlines and generated study sessions | [Todoist App Store listing](https://apps.apple.com/app/id572688855) |
| **Notion** (workspace with databases) | Databases of pages with properties such as dates and status; table, list, calendar, board and gallery views; filtering, sorting and grouping | Students must design and maintain their own databases and workflows to hold courses, assignments and exams, and the page we reviewed does not describe automatic scheduling. Smart Study Planner provides a ready structure for courses, assignments, exams, study hours and weekly planning | [Notion Help: Intro to databases](https://www.notion.com/help/intro-to-databases) |
| **Microsoft Teams for Education: Assignments** | Instructors create assignments with due dates; assignments are listed by nearest due date; they can be added to student calendars; scheduled posting | Only shows work that instructors post inside Teams classes, so exams, other platforms and personal study tasks are missing, and it has no study-time planning. Our Teams investigation (Section 4.5) is based on this | [Microsoft Support: Create an assignment in Teams](https://support.microsoft.com/education/create-an-assignment-in-microsoft-teams), [Schedule work to assign later](https://support.microsoft.com/en-US/education/schedule-work-to-assign-later) |
 
**What we learned.** The comparison shows that existing tools already handle dates, tasks and notifications well. Google Calendar supports calendar-based planning, Todoist focuses on tasks and priorities, Notion offers flexible databases, and Teams shows what instructors post. Four lessons shape our project:
 
1. **Placing study time is left to the student.** In the documentation we reviewed, none of the general tools generates a schedule from deadlines, estimated study hours and available time. This is the gap that FR-05 addresses.
2. **Flexible tools need setup.** Notion can hold academic data, but the student must build the structure, so we provide a fixed structure for courses, assignments and exams (FR-02 and FR-03).
3. **Reminders follow the task date.** Because notifications are tied to dates, a changed or cancelled date means the student must adjust their plan by hand. Our system updates reminders and study sessions automatically (FR-07 and FR-08).
4. **Teams covers only part of a student's workload.** Teams already adds instructor assignments to student calendars, so the planner should complement it, which is why we investigate Teams integration but do not depend on it.
The research also warns us to stay modest: a randomised trial with more than 9,000 college students found that an online weekly study planner and reminders increased studying slightly at some sites but had no measurable effect on grades or retention (Oreopoulos et al., 2022). We therefore present our planner as an organisation aid and do not promise better grades. Smart Study Planner does not aim to replace calendars or task managers. It combines academic task management with automatic study scheduling, and the first prototype relies on information entered by students instead of direct integration with other platforms. Our comparison relies on public documentation, so we do not claim that no such feature exists anywhere.
 
---
 
## 4. Proposed solution and justification
 
**What the system will do.** Smart Study Planner is a web application where students register their courses, enter assignments and exams (due date, weight, estimated hours, status), and see all deadlines in a single dashboard that highlights overdue and soon-due items. From the student's weekly availability, the estimated effort and a daily study limit that the student controls (default 4 hours, adjustable), the system generates a weekly study schedule using a simple rule-based algorithm: sessions are placed in free slots and prioritised by due date and weight. It suggests short breaks (for example 5 minutes after 25 minutes of study) and warns the student when the required study time is more than the available time, instead of silently adding more hours. When a student changes the date or time of an assignment or exam, or cancels it, the system **automatically updates** the reminders and the study schedule. The application also sends **reminders** (in the app and by email) before any assignment or exam, so students are warned even when they do not open the planner. Only students use the planner; administrators maintain courses and accounts.
 
**Who will use it.** Students (primary) and administrators. Instructors do not use the system.
 
**How it improves the current process.** Deadlines move from several scattered places into one view, a changed date is updated once and flows into the reminders and the schedule, reminders warn students before each assignment or exam, and the schedule shows when to work rather than only when work is due.
 
**Limitation of existing solutions that it addresses.** In the documentation we reviewed, Google Calendar, Todoist and Notion leave it to the student to place study time and to set up their own academic structure, and Teams Assignments only covers what instructors post in Teams. Our system targets the gap between them: deadlines from every course plus personal items plus reminders plus a generated study plan that updates when dates change.
 
**Responsible use.** The 4-hour default is a design choice for the prototype, not a medical or academic recommendation, and the student can change it at any time. The application will show this disclaimer: *Smart Study Planner is an academic planning tool. Study schedules are suggestions based on the student's available time and deadlines. Students can adjust their study hours and take breaks according to their personal needs. The application does not provide medical advice or guarantee academic results.*
 
**Why three students can finish a prototype.** The prototype is limited to three workflows and eight requirements. The scheduling logic is deliberately simple (a greedy, rule-based algorithm, not machine learning). Authentication, calendar display and email reminders will use existing libraries, and all data will be simulated.
 
**Reuse.** We plan to reuse open-source components: a web framework (for example React with Node.js/Express), a lightweight database (SQLite or PostgreSQL), an authentication library (for example JWT with bcrypt password hashing), a calendar component (for example FullCalendar), a job scheduler and email library for reminders (for example node-cron and Nodemailer with a test mail server), and GitHub Actions for automated tests. Final choices will be recorded in the design milestone.
 
---
 
## 5. Scope and workflows
 
| In scope (semester prototype) | Out of scope (will not be attempted this semester) |
|---|---|
| Web application with role-based login for Student and Administrator | Native mobile apps |
| Course catalogue maintained by an administrator (simple admin form or seed script) and student course selection | Real student, grade or university records; all data is simulated |
| Assignment and exam management with due date, weight, estimated hours and status | Automatic import from the university LMS or student information system |
| Deadline dashboard with sorting, filtering and overdue/soon-due highlighting | Grade calculation and GPA prediction |
| Rule-based weekly study schedule generation, rescheduling and completion tracking, with an adjustable daily study limit (default 4 hours), break suggestions and an overload warning | Machine-learning or AI-based schedule optimisation; medical or wellbeing advice |
| Automatic update of reminders and study schedule when a student changes the due date or time of an assignment or exam, or cancels it | Instructor accounts and instructor-published deadlines; SMS and mobile push notifications |
| Reminder notifications (in-app and email) before upcoming assignments and exams, with configurable lead times | Advanced notification rules, such as quiet hours or per-course custom rules |
| **Time-boxed investigation (about one week) of Microsoft Teams integration**, such as reading assignments through Microsoft Graph education APIs or exporting deadlines as a calendar file (.ics) that Teams/Outlook can import. It will be built only if the investigation shows it is feasible with our accounts and permissions | Full two-way Teams synchronisation, Teams bots or tabs |
 
| Workflow | Main actor and goal | Expected outcome |
|---|---|---|
| **W1: Set up my semester** | A student logs in, adds their courses, and enters assignments and exams with due dates, weights and estimated hours, to see everything in one place | All deadlines appear on the dashboard sorted by date, with overdue and due-within-48-hours items highlighted, and reminders are scheduled for each assignment and exam |
| **W2: Generate and follow a weekly study plan** | A student enters weekly availability and a daily study limit, and asks the system to plan study sessions before upcoming deadlines | A weekly schedule covering all upcoming deadlines is shown and saved, with break suggestions and a warning if the required study time exceeds the available time |
| **W3: Respond to a reminder and keep the plan up to date** | A student receives a reminder about an upcoming assignment or exam, then marks work as done, moves a study session, changes the due date or time, or cancels the assignment or exam | The dashboard, progress per course and schedule are updated; after a date change or cancellation, reminders and study sessions are updated or removed automatically |
 
---
 
## 6. Initial requirements
 
### Functional requirements
 
| ID | Functional requirement | Priority |
|---|---|---|
| FR-01 | The system shall authenticate users by university email and password and restrict each page and action according to the user's role (Student, Administrator). | Must |
| FR-02 | The system shall allow an authenticated student to add a course from the catalogue to their planner or remove it. | Must |
| FR-03 | The system shall allow a student to create, edit and delete an assignment or exam with course, due date and time, weight, estimated hours and status (not started, in progress, done, cancelled). | Must |
| FR-04 | The system shall display a student's deadlines on a dashboard sorted by due date, filterable by course and status, with overdue items and items due within 48 hours visually highlighted. | Must |
| FR-05 | The system shall generate a weekly study schedule based on the student's available time, upcoming deadlines, estimated study hours and daily study limit (default 4 hours, adjustable by the student), shall suggest breaks, and shall warn the student when the required study time exceeds the available time. | Must |
| FR-06 | The system shall allow a student to move a scheduled study session or mark it complete, and shall show the completion percentage for each course. | Should |
| FR-07 | The system shall send each student a reminder, as an in-app notification and by email, for every assignment or exam that is not marked done, at lead times the student can configure (default: 3 days and 1 day before the due date). | Must |
| FR-08 | The system shall automatically update the reminders and the study schedule when a student changes the due date or time of an assignment or exam, or cancels it: reminders are rescheduled or removed, and affected study sessions are recalculated or removed, without the student rebuilding the plan. | Must |
 
### Non-functional requirements
 
| ID | Category | Measurable requirement |
|---|---|---|
| NFR-01 | Performance | With the agreed demonstration dataset (6 courses, 60 tasks, 1 student), the dashboard shall load in 2 seconds or less and the weekly schedule shall be generated in 5 seconds or less, measured as the average of 20 test runs on a standard laptop. Each reminder (FR-07) shall be delivered within 1 minute of its scheduled time in a test of 20 scheduled reminders. After a due-date change or cancellation (FR-08), the affected reminders and study sessions shall be updated within 5 seconds in 20 of 20 test runs. |
| NFR-02 | Security and privacy | Passwords shall be stored only as salted hashes, and in a set of at least 15 automated authorisation tests (for example a student requesting another student's data or a student calling an administrator function), 100% shall be rejected. The system shall contain no real personal data. |
| NFR-03 | Usability and accessibility | In a usability test with at least 5 classmates, at least 4 shall complete Workflow W1 without help in 5 minutes or less, and the main pages (dashboard, task form, schedule) shall score 90 or higher in the Lighthouse accessibility audit. |
 
These are initial requirements. We will validate them with users and expand them in the requirements milestone.
 
---
 
## 7. Development approach
 
We choose a **hybrid approach: incremental development with short Agile iterations, combined with integration and configuration of existing components.** The overall need is stable: students must see deadlines and get a study plan. The details, such as how the schedule should look and what reminders are useful, are not yet known and are likely to change after students see a working version. A pure Waterfall plan would delay user feedback until the end of the semester, which is too risky for these unknowns. At the same time, the semester has fixed milestones, so we need a lightweight plan, not an open-ended one.
 
In practice, we will deliver the product as three increments, one per workflow (W1 setup and dashboard, W2 schedule, W3 reminders and plan updates), using two-week iterations. Each iteration starts with a short planning session, where requirements are taken from a GitHub Projects backlog, and ends with a demonstration to at least three classmates and a short review of their feedback, which changes the backlog. The team meets weekly, and every pull request is reviewed by a second member and must pass the automated tests before merging into `main`. The main risks are changing requirements, the uncertain Teams integration and limited time. We handle them by working in small increments, by time-boxing the Teams investigation to about one week, and by keeping the lowest-priority requirement (FR-06) as an item that can be dropped or simplified if we fall behind.
 
---
 
## 8. Team plan and risks
 
### Coordinator roles
 
| Role | Team member |
|---|---|
| Process and project coordinator | Loulwah Alsahali |
| Requirements and design coordinator | Malak Alenezi |
| Implementation and quality coordinator | Rifal Meshari Alkhudhair |
 
The roles coordinate the work. They do not divide it. All three members will write requirements, contribute design and code, test, and take part in each milestone and the final presentation.
 
### Milestone plan
 
| Milestone | Main planned output | Coordinator |
|---|---|---|
| 1. Proposal | `PROJECT_PROPOSAL.md`, `README.md`, repository, GitHub Projects backlog | Process and project coordinator |
| 2. Requirements and models | Validated requirements, use case diagram, workflow descriptions, data model, user feedback summary | Requirements and design coordinator |
| 3. Design and initial prototype | Architecture and screen design, working W1 (courses, tasks, dashboard) with login, result of the Teams investigation | Requirements and design coordinator (design), Implementation and quality coordinator (prototype) |
| 4. Final prototype, testing, and presentation | W2 and W3 completed, reminder notifications (FR-07), automatic updates after date changes and cancellations (FR-08), automated tests, NFR measurements, usability test, final demonstration and presentation | Implementation and quality coordinator |
 
### Risks
 
| Risk | Impact | Planned response |
|---|---|---|
| Requirements change after development starts, for example when classmates react to the prototype | High | Review the three workflows with at least three classmates before implementation; use two-week increments; keep a prioritised backlog and drop or simplify the "Should" item (FR-06) first; because FR-08 recalculates plans automatically, we will write automated tests for date changes and cancellations early |
| Microsoft Teams integration proves impossible because of permissions, tenant restrictions or missing API access for student accounts | Medium | Limit the investigation to about one week; keep Teams out of the core requirements; fall back to calendar-file (.ics) export or manual entry |
| Privacy and security of academic data, such as students entering real grades or course information, or an authorisation flaw exposing one student's data to another | High | Use only simulated or anonymised data; hash passwords; apply role checks on every request; run the authorisation tests in NFR-02 in every build; show a notice that the prototype is not for real data |
 
---
 
## 9. Sources, AI use, and contributions
 
### Sources
 
1. Google. "Create & manage tasks in Google Calendar" (Google Calendar Help). https://support.google.com/calendar/answer/6285327
2. Doist. "Todoist: To-Do List & Calendar" (App Store listing). https://apps.apple.com/app/id572688855
3. Notion Labs, Inc. "Intro to databases" (Notion Help). https://www.notion.com/help/intro-to-databases
4. Microsoft Support. "Create an assignment in Microsoft Teams." https://support.microsoft.com/education/create-an-assignment-in-microsoft-teams
5. Microsoft Support. "Schedule work to assign later." https://support.microsoft.com/en-US/education/schedule-work-to-assign-later
6. Patzak, A., Zhang, X., & Vytasek, J. (2025). Boosting productivity and wellbeing through time management: evidence-based strategies for higher education and workforce development. *Frontiers in Education, 10*. https://doi.org/10.3389/feduc.2025.1623228
7. Oreopoulos, P., Patterson, R. W., Petronijevic, U., & Pope, N. G. (2022). Low-touch attempts to improve time management among traditional and online college students. *Journal of Human Resources, 57*(1), 1–43. https://doi.org/10.3368/jhr.57.1.0919-10426R1
8. Planned reusable components (final selection in Milestone 3): React, Node.js/Express, SQLite or PostgreSQL, FullCalendar, bcrypt, JSON Web Tokens, GitHub Actions.
### Generative AI use
 
- **Tools:** Claude (Anthropic) and ChatGPT (OpenAI).
- **How they were used:** The team used both tools to gather information about the project idea (a study planner for university students) and to obtain the basic work steps for the proposal. With Claude, the team also drafted the proposal sections, the requirements, workflows and risk tables, and found candidate existing solutions and scholarly sources to review.
- **How the team verified and revised the output:** The team reviewed the AI output against the assignment brief (2 actors, 3 workflows, 8 functional requirements, 3 non-functional requirements, 3 risks) and revised it using our own experience as students. Based on how we actually manage deadlines and study time, we adjusted the problem description, requirements and scope to fit our project.
### Team contributions
 
| Member | Contribution to this proposal |
|---|---|
| Loulwah Alsahali | Drafted and reviewed Sections 1, 2 and 3 (team information, problem and users, existing solutions) |
| Malak Alenezi | Drafted and reviewed Sections 4, 5 and 6 (proposed solution, scope and workflows, initial requirements) |
| Rifal Meshari Alkhudhair | Drafted and reviewed Sections 7 and 8 (development approach, team plan and risks) |


