## Linear Ticket
<!-- Title and branch name must reference the Linear ticket (e.g. ENG-123) -->
- **Ticket**: [ENG-XXX](https://linear.app/counterpart-inc/issue/ENG-XXX)

---

## Description
<!-- Provide a concise description of the feature being added or the problem being solved. -->
- **Why is this change necessary?**
- **What does this PR do?**

**Type of Change**
- [ ] Bug fix
- [ ] New feature
- [ ] Refactor / cleanup
- [ ] Breaking change

---

## Pre-Submission Checklist
<!-- Complete all items before requesting review. Check each box or explain why it doesn't apply. -->
- [ ] Reviewer assigned

### Code Quality
- [ ] All Greptile blocking comments resolved (score: ___/5)
- [ ] Checksum coverage is verified; updated if needed

### Testing
- [ ] Unit tests added or updated
  <!-- List any unit tests added or updated. -->
- [ ] End-to-end / Playwright test added (if applicable — new user-facing flows)
  <!-- Link to test file(s) if applicable. -->

#### Manual Testing Steps
<!-- Step-by-step instructions so the reviewer can verify the functionality. -->
1.
2.
3.

#### QA Evidence
<!-- A Loom video is required when manual testing is needed. -->
- [ ] Loom video linked: <!-- paste URL -->
- [ ] Playwright trace linked: <!-- paste URL -->
- [ ] Screenshots attached (before / after)

### Safety & Rollback
- [ ] Feature flag in place **or** rollback strategy described below **or** EM approval comment added

---

## Release Management Checklist
<!-- Let the person responsible for releasing this know what to pay attention to. -->
- [ ] Added new endpoints or services
- [ ] Added new feature flags
- [ ] Added new environment variables <!-- update .env.example and notify DevOps -->
- [ ] Added new dependencies / packages
- [ ] Modified database schema <!-- note migration timing below: pre-deploy / post-deploy / zero-downtime -->
- [ ] Integrated with external service or API (if applicable)
- [ ] Made security-related changes
- [ ] Updated business logic for existing features

---

## Rollback Strategy
<!-- If no feature flag, describe how this change can be safely reverted. Leave blank if using a feature flag. -->

---

## Additional Notes
<!-- Any additional context, trade-offs, or considerations for reviewers. -->
