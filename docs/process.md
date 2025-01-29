---
title: Engineering Process
nav_order: 99
last_modified_date: 2025-01-20 12:00
---

# **Working with Engineers**

A guide to help the data team collaborate effectively with data engineers, streamline processes, and ensure smooth delivery of data-related tasks and projects.

---

## **Asana**

### **Daily Standups**
- **Purpose**: Share updates, clarify blockers, and align on priorities.
- **Best Practices**:
  - Keep updates concise! 
    - What was done yesterday? 
    - What’s planned for today? 
    - Blockers.
  - Use this time to sync on shared tasks or deadlines.
  - Highlight who engineers might be dependent on and who to go to for more information


{: .tip}
Ensure there is enough context. Consider having a chat outside the standups to ensure you fully understand the ask and the requirements.

### **Creating a New Request**
- **Purpose**: Clearly define requests for engineers
- **Steps**:
  1. Create a new task in Asana with a clear title
  2. Ensure steakholders are tagged on the ticket
  3. Include detailed descriptions:
     1. Objective of the request. This may include some detail of context.
     2. Specific data sources or tables needed.
     3. Expected output or deliverables. Clear outline of the completion criuteria.
     4. Deadline and/or priority level.
  4. Attach any relevenmt screenshots or documents

{: .tip}
For requests outside the London D&A team ensure an engineer is present in the breifing to reduce misunderstandings. 

### **Prioritisation of a Request**
- **Guiding Questions**:
  - How urgent is this request? (Does it block another team/project?)
  - What is the business impact? (Revenue, customer experience, etc.)
  - Are there dependencies or deadlines tied to this request?
- **Process**:
  - Non-Priorty tickets should be in the backlog. 
  - Priotity tickets (with the deadline in the next 2 weeks) should be in the Priority column
  - Assigned tasks should be estimated to be completed in the current week

{: .important}
When a ticket moves from the priority column to an Engineers column ensure this can still be addressed within the time period.

### **The Effort per Ticket**
- **Effort Estimation**:
  - Collaborate with engineers to understand what’s involved (e.g., is it a simple query or a new pipeline?).
  - Engineers ensure you are considering technical complexity, existing workloads, and dependencies.
- **Asana Ticket**: For tickets ensure a ticket can be completed within the day. Or have multiple sub-tasks that can be completed within a day. To demonstrate momentum and help breakdown tasks.

### **(Engineers) Understanding a Completion of a Request**
- **Clear Completion Criteria**:
  - Define what "done" means for each request (e.g., code merged, data verified, dashboards updated).
  - Agree on validation steps (e.g., peer reviews, testing, and sign-off from the requester).
- **Feedback Loop**:
  - Review completed tasks together and highlight any discrepancies or next steps.
  - Document learnings to improve future collaboration.

---

## **Quick Requests**
- **Purpose**: Handle small, urgent tasks efficiently without disrupting larger workflows.
- **Process**:
  - Tag small tasks with a "small but urgent" in the Asana ticket.
  - Define clear turnaround times
  - Limit quick requests to tasks that can be completed within 1 hour
- **Communication**: Use teams to clarify small requests without overloading standups.

{: .warning}
Aviod overloading Engineers with numerous _small quick tasks_

---

## **Big Projects**
- **Definition**: Larger, multi-phase initiatives requiring planning, resource allocation, and cross-team collaboration (e.g., building a new data warehouse, migrating systems, or creating complex ETL pipelines).
- **Steps for Collaboration**:
  1. Kickoff Meeting: Align on objectives, roles, and timelines.
  2. Detailed Specs: Provide a thorough problem definition, requirements, and any constraints upfront.
  3. Milestones: Break the project into phases with clear deliverables and review points.
  4. Regular Check-Ins: Schedule weekly or biweekly syncs to track progress and address blockers.
- **For Data Teams**: Proactively gather feedback from stakeholders to ensure the project aligns with business needs and share updates with engineers.
