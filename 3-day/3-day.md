# Confict Resolution
- [What can cause a conflict? ](#what-can-cause-a-conflict)
- [Cover strategies for conflict resolution](#cover-strategies-for-conflict-resolution)
- [Work in pairs: Create a new repo, create a conflict and practice conflict resolution](#work-in-pairs-create-a-new-repo-create-a-conflict-and-practice-conflict-resolution)
- [provide a step-by-step instruction for how to resolve a conflict](#provide-a-step-by-step-instruction-for-how-to-resolve-a-conflict)

## What can cause a conflict? 
**Merge conflicts happen when you merge branches that have competing commits, and Git needs your help to decide which changes to incorporate in the final merge.**

If the two branches you're trying to merge both changed the same part of the same file, Git won't be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.

The great part of Git's merging process is that it uses the familiar edit/stage/commit workflow to resolve merge conflicts. When you encounter a merge conflict, running the git status command shows you which files need to be resolved. For example, if both branches modified the same section of hello.py, you would see something like the following:
```bash
On branch main
Unmerged paths:
(use "git add/rm ..." as appropriate to mark resolution)
both modified: hello.py
```
### Types of merge conflicts
1. **Git fails to start the merge**<br>
A merge will fail to start when Git sees there are changes in either the working directory or staging area of the current project. Git fails to start the merge because these pending changes could be written over by the commits that are being merged in. When this happens, it is not because of conflicts with other developer's, but conflicts with pending local changes. The local state will need to be stabilized using `git stash`, `git checkout`, `git commit` or `git reset`. 
```bash
error: Entry '<fileName>' not uptodate. Cannot merge. (Changes in working directory)
```
2. **Git fails during the merge**<br>
A failure DURING a merge indicates a conflict between the current local branch and the branch being merged. This indicates a conflict with another developers code. Git will do its best to merge the files but will leave things for you to resolve manually in the conflicted files.
```bash
error: Entry '<fileName>' would be overwritten by merge. Cannot merge. (Changes in staging area)
```

## Cover strategies for conflict resolution

There are a few steps that could reduce the steps needed to resolve merge conflicts in Git.

- Step 1: The easiest way to resolve a conflicted file is to open it and make any necessary changes.

- Step 2: After editing the file, we can use the git add a command to stage the new merged content.

- Step 3: The final step is to create a new commit with the help of the git commit command.

- Step 4: Git will create a new merge commit to finalize the merge.


## Branching Rules:

**Regex Rule:** Enforces branch naming conventions in specified project groups.

**Project Groups:** Include shared services, infrastructure, Kubernetes, and platform.

**Feature Branch:**

- **Ownership:** Developers for regular feature development.
- **Creation:** Based on JIRA ID and subject short name.
- **Workflow:** Creation from Development Base Branch. Includes development, squashing, rebasing, testing, and merge request creation. Back-porting involves creating branches from release branches, cherry-picking commits, resolving conflicts, and following a similar workflow.

**Hotfix Branch:**

- **Ownership:** Developers for urgent fixes on production.
- **Naming Convention:** Similar to feature branches with specific restrictions.
- **Workflow:** Creation from Release Branch. Involves hotfix implementation, squashing, rebasing, testing, and merge request creation. Porting hotfixes involves similar steps but with branches created from the Development Base Branch.

**Release Branch (Optional):**

- **Purpose:** Maintains major versions released to production.
- **Creation:** Decision made by Release Manager and SW Product Owner.
- **Workflow:** Creation from a specific commit in Development Base Branch, including agreed features/bugfixes.

**Development Branch:**

- **Purpose:** Used for joint work on future versions.
- **Functionality:** Allows breaking backward compatibility (to be accepted by the owner).
- **Tags:** Primarily owned by Release Manager, with exceptions for temporary tags by developers.

**Configuration Checklist for GitLab Projects:**

**Merge Method:**

- Use fast-forward merge method.

**Delete Source Branch:**

- Always delete the source branch on merge.

**Squash Commits:**

- Always squash the source branch before merging.

**Merge Checks:**

- Only allow merge requests if the pipeline succeeds and all threads are resolved.

**Branch Deletion Option Confirmation:**

- Confirm the option to delete branches on merge during merge request creation.

**Email Notifications on Failed Pipelines:**

- Enable email notifications for failed pipelines.
- Failed pipeline notifications sent to the author of the pipeline.

**Manual Stages in Pipelines:**

- Monitor pipelines with manual stages (defined with "when: manual" clause).
- Ensure manual steps are executed by pushing the Play button to prevent post-merge steps affecting infrastructure.

**Infrastructure Housekeeping:**

- Perform housekeeping for infrastructure, like destroying resources using tools such as Terraform.

**Allow Failure Setting:**

- Set allow_failure to false for housekeeping stages in .gitlab-ci.yml.
- Ensure notifications for failures are received via email or Slack channels.
