---
title: Version Control
parent: Engineering Standards
nav_order: 6
last_modified_date: 2025-01-20 12:00
---

# Version Control Practices

Effective version control practices help maintain project stability, encourage collaboration, and ensure a seamless development workflow. Below are detailed guidelines for managing branches, commits, and pull requests.

---

## Branching Strategy

A consistent and clear branching strategy minimizes conflicts and ensures orderly development. Consider implementing the following structure:

1. **Main Branch**
   - This is the **production-ready branch** that contains stable, release-quality code.
   - Enable **branch protection rules** to prevent direct commits:
     - Require Pull Requests (PRs) for all changes.
     - Ensure all tests pass and code reviews are completed before merging.
   - Only merge code from feature, release, or hotfix branches after thorough testing.

2. **Feature/Bugfix Branches**
   - Use dedicated branches for each new feature or bugfix to isolate work and prevent unintended impacts.
   - **Naming Convention**:
     - Prefix branch names with a type (e.g., `feature`, `bugfix`) and optionally include the contributor’s initials:
       - Example: `alvi/feature/add-dark-mode`, `alvi/bugfix/fix-api-error`.
   - Focus on keeping changes in these branches small and relevant to a single task.

3. **Release Branches**
   - Use release branches (e.g., `release/v1.0`) to prepare for a version milestone or deployment.
   - These branches allow for final testing and adjustments without interrupting ongoing feature development.
   - Once validated, merge the release branch into `main`.

4. **Hotfix Branches**
   - Create hotfix branches for urgent, critical fixes affecting production (e.g., `hotfix/resolve-payment-bug`).
   - Merge hotfixes back into `main` and any other active branches (e.g., `dev`, `release`).

5. **Development (Optional)**
   - For complex workflows, maintain a `dev` branch as an integration point for new features and fixes before merging to `main`.
   - Use this branch for testing and validation across the team.

---

## Descriptive Commits

Commit messages are vital for understanding the history of a project. Well-structured messages improve collaboration and make debugging easier.

### Best Practices for Commit Messages
1. **Follow the Conventional Commits Format**
   - Use a consistent pattern for all commits:
     ```
     <type>(<scope>): <short description>
     ```
     - **type**: The nature of the change (e.g., `feat`, `fix`, `docs`, `refactor`, `test`, `chore`).
     - **scope**: The module, feature, or area impacted by the change (e.g., `auth`, `cart`).
     - **short description**: A concise summary of the change.
   - Example:
     - Good: `feat(api): add user authentication middleware`
     - Poor: `updated code`

2. **Provide Additional Context**
   - For complex changes, add more details in the commit body:
     ```
     fix(cart): resolve item duplication issue

     - Refactored the add-to-cart logic to prevent duplicate items.
     - Added test cases to cover this edge case.
     ```

3. **Commit Frequently and Logically**
   - Break your changes into smaller, logical commits.
   - Avoid bundling unrelated changes into a single commit.
