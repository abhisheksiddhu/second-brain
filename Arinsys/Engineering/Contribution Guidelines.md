General contribution guidance is included in this document. Additional guidance is defined in the documents linked below.

# DOs and DON'Ts

Please do:

- DO follow our Coding Guidelines
- DO give priority to the current style of the project or file you're changing even if it diverges from the general guidelines.
- DO include tests when adding new features. When fixing bugs, start with adding a test that highlights how the current behavior is broken.
- DO keep the discussions focused. When a new or related topic comes up it's often better to create new issues than to sidetrack the discussion.

Please do not:

- DON'T make PRs for style changes.
- DON'T surprise us with big pull requests. Instead, file an issue and start a discussion so we can agree on a direction before you invest a large amount of time.
- DON'T commit code that you didn't write. If you find code that you think is a good fit to add to the project, file an issue, and start a discussion before proceeding.

---

# Pull Requests

- DO submit all code changes via pull requests (PRs) rather than through a direct commit. PRs will be reviewed and potentially merged by the repo maintainers after a peer review that includes at least one maintainer.
- DO NOT submit "work in progress" PRs. A PR should only be submitted when it is considered ready for review and subsequent merging by the contributor.
- DO give PRs short-but-descriptive names (e.g. "Improve code coverage for Authentication Service by 10%", not "Fix #1234")
- DO refer to any relevant issues, and include [keywords](https://help.github.com/articles/closing-issues-via-commit-messages/)  that automatically close issues when the PR is merged.
- DO tag any users that should know about and/or review the change.
- DO ensure each commit successfully builds. The entire PR must pass all tests in the Continuous Integration (CI) system before it'll be merged.
- DO address PR feedback in an additional commit(s) rather than amending the existing commits and only rebase/squash them when necessary. This makes it easier for reviewers to track changes.
- DO assume that ["Squash and Merge"](https://github.com/blog/2141-squash-your-commits)  will be used to merge your commit unless you request otherwise in the PR.
- DO NOT fix merge conflicts using a merge commit. Prefer `git rebase`.
- DO NOT mix independent, unrelated changes in one PR. Separate real product/test code changes from larger code formatting/dead code removal changes. Separate unrelated fixes into separate PRs, especially if they are in different assemblies.

---

# Commit Messages

Please format commit messages as follows (based on [A Note About Git Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) ):

```PlainText
#[ticket_id], #[ticket_id_2] Summarize change in 50 characters or less

Provide more detail after the first line. Leave one blank line below the
summary and wrap all lines at 72 characters or less.

If the change fixes an issue, leave another blank line after the final
paragraph and indicate which issue is fixed in the specific format
below.

Fix #[ticket_id]
```

Also do your best to factor commits appropriately, not too large with unrelated things in the same commit, and not too small with the same small change applied N times in N different commits.

---

# Branch Management

## Branch Organization

We use separate branches for the development of all new features. After all the features are done in a separate branch they will be merged into the `main` branch.

Development branches follow the naming based on the milestone version number. For example, if the milestone is `1.2.3` the main development branch will be named `dev-1.2.3` and all feature branches will be based on `dev-1.2.3`. Feature branches follow the naming `dev-1.2.3-feature-name`.

## Branching Policies

- All branches will be deleted as soon as it gets merged back to their parent branch
- All code to the main branch can only go through a Pull request to facilitate code review and prevent accidental check-ins
- Pull Requests to the main branch can be self-approved by maintainers to allow hotfixes.
- All Pull Requests will do a squash merge.

---

# Coding Style

- Every project should have an editor config file that includes all the recommended styling rules set. Format your code accordingly before committing.