---
title: Pull Requests Practices
parent: Engineering Standards
nav_order: 5
last_modified_date: 2025-01-20 12:00
---

# Pull Requests (PRs)

Pull requests facilitate collaboration, reviews, and testing before code integration. They ensure that changes are well-documented, reviewed, and aligned with project standards.

---

## For the Committer

1. **Create Descriptive Titles and Summaries**
   - Example PR Title: `Add feature flag for beta features`.
   - PR Description:
     - **Why**: Explain the reason for the change.
     - **What**: Summarize key updates introduced.
     - **How**: Provide testing details or special considerations.

2. **Perform a Self-Review**
   - Ensure the following before submitting:
     - Code adheres to style and quality standards.
     - All tests pass successfully.
     - Documentation is updated where needed (e.g., `CHANGELOG.md`, `README.md`).

3. **Link Related Issues**
   - Reference issues or tasks in the description:
     ```
     Closes #123 - Adds payment gateway support.
     ```

4. **Add Reviewers and Labels**
   - Tag relevant team members as reviewers.
   - Apply labels to indicate:
     - **Type**: `bug`, `enhancement`, `documentation`.
     - **Priority**: `high`, `medium`, `low`.
     - **Status**: `ready for review`, `WIP`.

---

## For the Reviewer

1. **Review Thoroughly and Constructively**
   - Assess the code for:
     - **Functionality**: Does it solve the problem?
     - **Readability**: Is the code clear and maintainable?
     - **Performance**: Are there bottlenecks or inefficiencies?
   - Provide actionable feedback:
     - **Specific**: "Refactor this loop to use a generator for better memory efficiency."
     - **Encouraging**: "Great implementation! Consider adding a test case for edge conditions."

2. **Verify Code Quality**
   - Ensure adherence to coding standards.
   - Suggest improvements, such as modularity or naming clarity.

3. **Approve or Request Changes**
   - Approve the PR only when all issues are resolved and standards are met.
   - Clearly articulate required updates when requesting changes.

4. **Provide Timely Feedback**
   - Avoid delays in the review process to maintain workflow efficiency.

---

## Pull Request Review Guidelines

To streamline the review process, reviewers focus on the following areas:

### Key Review Areas

1. **Code Quality**
   - Avoid hardcoding; use functions, classes, and reusable components.
   - Ensure logical organization of files and meaningful file names.

2. **Runtime Efficiency**
   - Identify potential runtime issues (e.g., unnecessary loops, unoptimized libraries).
   - Suggest performance improvements where applicable.

3. **Variable Naming**
   - Use descriptive and meaningful names (e.g., `campaign_data` instead of `df`).

4. **Methodology**
   - Recommend better techniques, such as list comprehensions over loops where appropriate.

5. **Documentation**
   - Ensure docstrings follow the **Sphinx** style, including inputs, outputs, and examples.

6. **Code Clarity**
   - Flag confusing code blocks and request clarifications or comments.

### After the Review

1. **Request Changes**
   - Identify required changes with actionable feedback.

2. **Comment on Enhancements**
   - Highlight optional improvements for future iterations.

3. **Approve or Request Further Changes**
   - Approve the PR if all changes meet standards or request additional revisions if necessary.

---

