---
title: Engineering Process
nav_order: 99
last_modified_date: 2025-01-29 12:00
---

# Working with Engineers

We are a pain-in-the-arse to work with. So here are some things that hopefully will make life easier for us all. 

## Asana

The Engineering Standup [Board](https://app.asana.com/0/1207400211954260/1207400871321914) is designed to organise and prioritise tasks efficiently. Here’s how it works:

### Task Columns
- **Backlog**: Tasks that are not urgent and can be addressed in the future.
- **Priority**: High-priority tasks that need immediate attention, typically with deadlines within the next two weeks.
- **Blocked**: Tasks that are awaiting external input or resolution.
- **To Review**: Completed tasks that need stakeholder or team member review.
- **Completed**: Tasks that have been reviewed, validated, and officially finished.

Each engineer has their own column to track active and assigned tasks. Tasks move into an engineer’s column when they are ready to be picked up from the **Priority** column. The goal is to maintain focus and ensure engineers are not overloaded, with no more than 2–3 tasks assigned at any given time.

{: .important}  
Use this board as the single source of truth for task status, ownership, and priority order to ensure alignment across the team. Link Engineering tickets to other boards as necessary.

---

## Additional Asana Fields

To improve clarity and tracking, the following fields should be included in every Asana task:

- **POC**: Point of contact for any context or information needed on the task. This ensures there is always a go-to person for questions or clarifications.
- **Sign-off**: The individual or team responsible for reviewing and confirming the task is complete. This ensures accountability and clear handover points.
- **Progress**: A status indicator to track the task’s progress:
  - **On Track**: The task is progressing as expected and is on track for the estimated delivery date.
  - **At Risk**: The task is not progressing as planned, is blocked by other tickets, or may miss the expected deadline. This flag helps raise awareness early.
  - **Overdue**: The task is running past the expected due date. This highlights tasks that need immediate attention.
- **Effort**: The total estimated effort (in hours or story points) required to complete the task.
- **Remaining Effort**: The estimated effort remaining to complete the task. This helps track progress and adjust priorities if needed.

These fields provide better visibility into task status, ownership, and progress, enabling smoother collaboration and timely delivery.

---

## Meetings

Engineering has three types of meetings:

1. **Daily Standups (15 mins)**: Share updates, address blockers, and align on priorities.
2. **Bi-Weekly Review (40 mins)**: Reflect on the team's progress, reprioritise the backlog, and align on upcoming tasks.
3. **Engineering Regroup (60 mins)**: Address tasks that need to be done on product days.

### Daily Standups
- **Purpose**: Share updates, address blockers, and align on priorities.
- **Best Practices**:
  - Keep updates concise:
    - What was done yesterday?
    - What’s planned for today?
    - Are there any blockers?
  - Use this time to align on shared tasks or deadlines.
  - Highlight dependencies and clearly identify who to approach for further details.
  - **Completion Flags**: Flag completed tickets explicitly during standups to ensure clarity.

{: .tip}  
Ensure enough context is provided. <br>If necessary, have follow-up conversations outside of standups to fully understand the ask and requirements.

---

### Bi-Weekly Sprints
- **Purpose**: Understand the workload for the next two weeks. Reprioritise backlog and balance client workload.
- **Best Practices**:
  - Ensure there is a manageable list of tasks within the priority list.
  - Ensure the list of tasks can be completed within the two-week sprint.
  - Reprioritise tasks based on current workloads.
  - Share estimated story points (hours) on each ticket.

---

## Creating a New Request
- **Purpose**: Provide clear and detailed requests to engineers.
- **Steps**:
  1. Create a new task in Asana with a descriptive title.
  2. Tag all relevant stakeholders on the ticket (so they get updates).
  3. Include a detailed description, covering:
     - **Objective**: Explain the purpose of the request, including key context.
     - **Specific data sources or tables**: Clearly outline the required inputs.
     - **Expected output**: Define deliverables and completion criteria. If there is a data discrepancy issue, input the expected figure.
     - **Deadline and priority level**: Specify timelines.
  4. Attach any relevant screenshots or documentation.
  5. Populate the additional Asana fields:
     - **POC**: Identify the point of contact for the task.
     - **Sign-off**: Specify who will review and confirm completion.
     - **Progress**: Set the initial status (e.g., "On Track").
     - **Effort**: Provide an estimated effort for the task.
     - **Remaining Effort**: Initially, this will match the total effort.

{: .important}  
For requests outside the London D&A team, ensure an engineer attends the briefing to reduce misunderstandings.

---

## Prioritisation of a Request
- **Guiding Questions**:
  - How urgent is this request? (Does it block another team or project?)
  - What is the business impact? (E.g., revenue or customer experience impact?)
  - Are there dependencies or deadlines tied to the request?
  - When shifting a priority ticket to an engineer’s column, question: How does this relate to current tickets?

- **Process**:
  - Non-priority tasks should remain in the backlog.
  - Priority tasks (with deadlines within the next two weeks) should be placed in the **Priority** column.
  - Tasks assigned to engineers should be planned to be completed within the current week.
  - Tasks assigned to engineers should be limited to 2–3 active tickets at a time to avoid overloading.

{: .important}  
When moving a ticket from the **Priority** column to an engineer’s column, confirm that it can still be addressed within the time frame.

---

## Effort per Ticket
- **Effort Estimation**:
  - Collaborate with engineers to understand what’s involved (e.g., is it a simple query or a new pipeline?).
  - Engineers should factor in technical complexity, existing workloads, and dependencies when estimating effort.
- **Asana Tickets**:
  - Each engineer should ideally have **no more than 2–3 tickets in progress** at a time.
  - For larger tasks, use subtasks that can be completed within a day to break down the work, demonstrate progress, and maintain momentum.

---

## Understanding Completion of a Request
- **Clear Completion Criteria**:
  - Define what "done" means for the request (e.g., code merged, data verified, dashboards updated).
  - Agree on validation steps such as peer reviews, testing, and sign-off from the requester.
- **Feedback Loop**:
  - Review completed tasks together, highlighting any discrepancies or next steps.
  - Document lessons learned to refine future collaboration.

---

## Quick Requests
- **Purpose**: Efficiently handle small, urgent tasks without disrupting ongoing work.
- **Process**:
  - Tag tasks as "small but urgent" in Asana.
  - Define clear turnaround times for these requests.
  - Limit quick requests to tasks that can be completed within an hour.
- **Communication**: Use direct communication (e.g., Teams or Slack) to clarify details quickly without taking time during standups.

{: .warning}  
Avoid overwhelming engineers with too many small, urgent tasks.

---

## Tickets Lagging
- **Problem**: Depending on external priorities, some tickets may not progress.
- **Steps**:
  1. During standups, flag any priority tickets that haven’t seen progress for over two weeks.
  2. Ensure requirements are clear.
  3. Escalation process:
     1. Ensure the ticket is clear and in the prioritised list (needs to be completed in the next two weeks).
     2. In daily standups, prioritise your client tickets.
     3. Flag in daily standup if there is no progress.
     4. Flag in the Monday Standup to reprioritise client-engineering resource.
     5. Have an "Overdue" flag to allow reminders to prioritise.

{: .tip}  
The bi-weekly sprints should allow backlog grooming and review sessions to review tickets that haven’t moved and decide whether they should be closed, updated, or reprioritised.

---

## One Client Hogging Resources
- **Problem**: A single client or project consuming too much of the team’s bandwidth can lead to other priorities being neglected. This imbalance can create delays in other workstreams and impact overall productivity.
- **Steps**:
  1. Monitor workloads for each client, ensuring there is enough resource being allocated cross-clients.
  2. Give clear priority based on impact and deadline.
  3. Track time being spent on tickets and projects.
  4. Raise awareness!

{: .important}  
In bi-weekly sessions, rebalance client priorities to ensure fair distribution.

---

## Big Projects
- **Definition**: Large-scale, multi-phase initiatives that require planning, resource allocation, and collaboration (e.g., building a new data warehouse, migrating systems, or designing complex ETL pipelines).
- **Steps for Collaboration**:
  1. **Kickoff Meeting**: Align on objectives, roles, and timelines.
     - Identify each engineer's **speciality** to assign roles that best match their strengths.
  2. **Detailed Specs**: Clearly define the problem, requirements, and any constraints upfront.
  3. **Milestones**: Break the project into manageable phases with clear deliverables and review checkpoints.
  4. **Regular Check-Ins**: Schedule weekly or biweekly syncs to track progress and address blockers.
- **For Data Teams**:
  - Regularly gather feedback from stakeholders to ensure the project aligns with business goals.
  - Keep engineers informed about changes in priorities or requirements.

