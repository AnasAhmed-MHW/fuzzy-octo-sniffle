---
title: Engineering Process
nav_order: 99
last_modified_date: 2025-01-29 12:00
---

# Working with Engineers

We are a pain-in-the-arse to work with. So here are some things that hopefully will make life easier for us all. 

## Asana

The Engineering Standup [Board](https://app.asana.com/0/1207400211954260/1207400871321914) is specifically designed to organise and prioritise tasks efficiently.

These columns categorise tasks based on their current status or workflow stage:  
- **Backlog**: Tasks that are not urgent and can be worked on in the future.  
- **Priority**: High-priority tasks that need immediate attention, typically with deadlines in the next two weeks.  
- **Blocked**: Tasks that are blocked by someone outside the data team and is awaiting response. 
- **To Review**: Tasks that are completed but need to be reviewed or validated by a stakeholder or team member before being marked as done.  
- **Completed**: Tasks that have been reviewed, validated, and officially finished.

Each engineer has their own column to track their active and assigned tasks. Tasks move into an engineer’s column when they are ready to be picked up from the **Priority** column. The goal is to maintain focus and ensure engineers are not overloaded, with no more than 2–3 tasks assigned at any given time.  

{: .important}  
Use this board as the single source of truth for task status, ownership, and priority order to ensure alignment across the team. Link Engineering ticket to other boards as necessity. 

---

## The Meetings

Engineering have 3 types of meetings:

1. Dialy Standups (15mins): Share updates, address blockers, and align on priorities 
2. Bi-Weekly Review (40mins): Reflect on the team's progress, reprioritise the backlog, and align on upcoming tasks
3. Tech Debt (60mins): Address underlying technical issues or inefficiencies that impact the team's ability to deliver.

## Daily Standups 
- **Purpose**: Share updates, address blockers, and align on priorities.  
- **Best Practices**:  
  - Keep updates concise!
    - What was done yesterday?
    - What’s planned for today? 
    - Are there any blockers?
  - Use this time to align on shared tasks or deadlines.  
  - Highlight dependencies and clearly identify who to approach for further details.
  - **Completion Flags**: Flag completed tickets explicitly during standups to ensure clarity 

{: .tip}  
Ensure enough context is provided. If necessary, have follow-up conversations outside of standups to fully understand the ask and requirements.  

---

## Creating a New Request
- **Purpose**: Provide clear and detailed requests to engineers.  
- **Steps**:  
  1. Create a new task in Asana with a descriptive title.  
  2. Tag all relevant stakeholders on the ticket.  
  3. Include a detailed description, covering:  
     - **Objective**: Explain the purpose of the request, including key context.  
     - **Specific data sources or tables**: Clearly outline the required inputs.  
     - **Expected output**: Define deliverables and completion criteria.  
     - **Deadline and priority level**: Specify timelines.  
  4. Attach any relevant screenshots or documentation.  

{: .important}  
For requests outside the London D&A team, ensure an engineer attends the briefing to reduce misunderstandings.  

---

## Prioritisation of a Request
- **Guiding Questions**:  
  - How urgent is this request? (Does it block another team or project?)  
  - What is the business impact? (E.g., revenue or customer experience impact?)  
  - Are there dependencies or deadlines tied to the request?  
  - When shifting a priority ticket to an engineers column. Question: How does this relate to current tickets.

- **Process**:  
  - Non-priority tasks should remain in the backlog.  
  - Priority tasks (with deadlines within the next two weeks) should be placed in the **Priority** column.  
  - Tasks assigned to engineers should be planned to be completed within the current week. 
  - Tasks assigned to engineers should be limited to 2–3 active tickets at a time to avoid overloading. 

{: .important}  
When moving a ticket from the **Priority** column to an engineer’s column, confirm that it can still be addressed within the time frame.  

---

## The Effort per Ticket  
- **Effort Estimation**:  
  - Collaborate with engineers to understand what’s involved (e.g., is it a simple query or a new pipeline?).  
  - Engineers should factor in technical complexity, existing workloads, and dependencies when estimating effort.  
- **Asana Tickets**:  
  - Each engineer should ideally have **no more than 2–3 tickets in progress** at a time
  - For larger tasks, use subtasks that can be completed within a day to break down the work, demonstrate progress, and maintain momentum.  

---

## (Engineers) Understanding a Completion of a Request
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

- **Problem**: Depending on external prioirties some tickets may not progress.  
- **Steps**:  
  1. During standups, flag any priority tickets that haven’t seen progress for over two weeks
  2. Ensure requirements are clear
  3. Escalation process
     1. Ensure ticket is clear and in the prioritised list (Needs to be completed in the next two weeks)
     2. In daily standups prioritise your client tickets
     3. Flag in daily standup if there is no progress 
     4. Flag in the Monday Standup to repriotise client-engineering resource
     5. Have an "Overdue" flag to allow reminders to pririotse.

{: .tip}
Schedule bi-weekly backlog grooming and review sessions to review tickets that haven’t moved and decide whether they should be closed, updated, or reprioritised


---


## One Client hogging resource
- **Problem**: A single client or project consuming too much of the team’s bandwidth can lead to other priorities being neglected. This imbalance can create delays in other workstreams and impact overall productivity  
- **Steps**:  
  1. Monitor workloads for each clienbt ensuring there is enough resource being allocated cross-clients
  2. Give clear priority based on impact and deadline
  3. Track time being spent on ticketsd and projects
  4. Raise awareness!

{: .important}
In bi-weekly sessions rebalance client priorities to ensure fair distribution.

---

## Big Projects
- **Definition**: Large-scale, multi-phase initiatives that require planning, resource allocation, and collaboration (e.g., building a new data warehouse, migrating systems, or designing complex ETL pipelines).  
- **Steps for Collaboration**:  
  1. **Kickoff Meeting**: Align on objectives, roles, and timelines.  
    - Identify each engineer's **speciality** to assign roles that best match their strengths
  2. **Detailed Specs**: Clearly define the problem, requirements, and any constraints upfront.  
  3. **Milestones**: Break the project into manageable phases with clear deliverables and review checkpoints.  
  4. **Regular Check-Ins**: Schedule weekly or biweekly syncs to track progress and address blockers.  
- **For Data Teams**:  
  - Regularly gather feedback from stakeholders to ensure the project aligns with business goals.  
  - Keep engineers informed about changes in priorities or requirements.  

