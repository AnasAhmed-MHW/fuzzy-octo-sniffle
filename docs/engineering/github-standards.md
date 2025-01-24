---
title: GitHub Best Practices
parent: Engineering Standards
nav_oder: 2
last_modified_date: 2025-01-20 12:00
---

# GitHub Best Practices

This document outlines best practices for collaborating on GitHub repositories within the MB Mediahub organisation. It serves as a guide for developers, reviewers, and admins to maintain code quality, streamline collaboration, and ensure repository consistency

### New Organisation  
We have transitioned to the **MB Mediahub** Organisation on GitHub. Please migrate repositories from the old Organisation to the new one:  
- **New Organisation**: [MB Mediahub GitHub](https://github.com/Mediabrands-MHW-LDN-Github)  
- **Old Organisation**: [Old GitHub](https://github.com/mediahub-london)  

---

### Branch Management  
- The `main` branch is protected from direct commits to maintain repository integrity.  
- **Pull Request (PR) approval** is required to merge changes into the `main` branch.  
  - Admins have bypass capability for urgent situations (e.g., fixing typos), but this should be used sparingly.  

---

### Collaboration Guidelines  
- **Branching and Pull Requests**:  
  - Use feature branches (`feature/branch-name`) or bugfix branches (`bugfix/branch-name`) for development.  
  - Submit PRs for all changes to ensure review and maintain collaboration transparency.  
- **Code Formatting**:  
  - Use the **Black formatter** to ensure consistent coding style across Python projects.  
  - Pre-commit hooks are recommended to enforce formatting before commits.  
- **Real-Time Collaboration**:  
  - For parallel work, utilize tools like **VSCode Live Share** for real-time code updates and seamless collaboration.  

---

### Pull Request (PR) Guidelines  
When submitting a PR:  
1. **Include Context**:  
   - Reference relevant **issues** in the PR description to help reviewers understand the purpose of the changes.  
2. **Databricks-Specific Repos**:  
   - Commit Databricks notebooks in their `.py` version for compatibility.  
3. **Testing**:  
   - Indicate whether the code has been tested and, if possible, provide details about the test cases and outcomes.  
4. **Focus Areas**:  
   - Mention any specific sections you want the reviewer to focus on, e.g., new algorithms, integrations, or critical refactors.  

---

### Additional Notes  
- Regularly update dependencies to ensure compatibility and security.  
- Use GitHub Actions or similar CI/CD tools to automate testing and linting for all PRs.  
- Maintain clear and concise commit messages (e.g., `Add logging to user authentication module`).  
- Keep the repository documentation (e.g., README, CONTRIBUTING) updated for better onboarding and usability.  

