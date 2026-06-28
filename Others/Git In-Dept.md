#personal 
# Theory
1. The difference between local and remote repository is fundamental: Local commits only exist on the machine. Only through git push do they become visible to the team. This means: As many local commits can be made before they are pushed all at once

2. When a `git merge` results in conflict(s), we can either resolve the conflict(s) manually or abort the merge(see command 3)

3. New features are developed on `feature/<feature-name>` branches, pushed to the remote branch and then merged with main after a PR is accepted

4. When the production goes down, a standard is to create a hotfix branch, eg, `hotfix/security-patch`. The remaining workflow is same as merging a branch, push to remote branch -> switch to main -> merge -> resolve conflicts if any

5. Release branches are used in Git Flow to prepare production releases. They allow final bug fixes and documentation updates without blocking ongoing development. The release is tagged for easy reference and rollback if needed, eg `release/2.0.0`

6. When merge conflicts occur, the different versions are labelled as follows
		```
		<<<<<<< HEAD 
		(your changes) 
		======= 
		(other's changes) 
		>>>>>>> abc1234
		```
	To resolve, the conflict, edit the file and remove the conflict markers (`<<<<<<`, `=======` and `>>>>>`)

7. Consider a case where we have to undo a previous commit. `git reset --soft HEAD~1` removes the last commit. Similarly, `git reset --soft HEAD~n` removes the  last n commits. We can consider commits as elements in a stack. In this case, the commits are moved to the staging area. `git reset --soft HEAD` does nothing

8. `git reset --hard` removes the commits but does not preserve them in the staging area. Commits are deleted from history, ALL file changes are deleted, Working directory is cleaned, Staging area is cleared and there is no undo. It works in the same way `soft` does however `git reset --hard HEAD~n` will destroy the last `n` commits. `--hard` is used when Experiment failed, throw it away, Broke everything, need to start over, Committed secrets/passwords by accident, NOT on commits already pushed, NOT if the changes might be needed later

9. Using `git reset --<soft/hard> HEAD~n`, ie, the 'n' notation is error-prone and confusing. A better alternative is to use `git reset --<soft/hard> <commit-hash>`, which enables resetting of a particular commit identified by its hash. ==Note: only the first 7 characters of the hash are required==

10. Consider a situation when development needs to be paused in order to work on a hotfix. `git stash` can be used to store the work in a special location, clean the workspace and switch tasks. When the task(development in this case) has to be resumed again, `git stash pop` can be used

11. While merging combines histories, rebasing rewrites it by moving the commits to appear after the commits from another branch. This creates a more linear, cleaner history.Rebasing is often preferred to maintain a clean, linear project history. Many teams use it to integrate feature branches before merging them to the main branch.

12. Just like merging, rebasing can lead to conflicts, but resolving conflicts during a rebase can be more complex because Git applies each of your commits one by one. A rebase can be aborted if resolving the conflict becomes too complex

13. Git offers a powerful tool called interactive rebasing to modify commit history. Small commits can be combined, commit messages reworded, or even deleted entirely. Interactive rebasing is commonly used to create a clean, coherent commit history before merging feature branches. This makes the codebase history more readable and meaningful.


14. Someone else might push changes to the main branch during development. Before the work is merged, these latest changes must be incorporated. Instead of merging main into the development(or any other) branch, which creates a merge commit, it is recommended to rebase the development branch onto main. This keeps the history cleaner. In collaborative environments, main branches are frequently updated. Rebasing feature branches onto main is a common workflow that helps avoid merge conflicts and keeps feature branches up to date.

15. Tags are like bookmarks in your Git history - they mark important points like releases. Unlike branches that move with new commits, tags stay fixed. In professional teams, every production release gets tagged. It's essential for debugging, rollbacks, and changelogs. Tags are industry standard for marking releases. They enable semantic versioning (v1.0.0), make rollbacks safe, and help teams communicate about specific versions.

16. `git show` is a fundamental tool for code review and debugging. It's used constantly in pull requests and when investigating issues. t shows you everything about a commit: the message, who made it, when, and most importantly, the actual code changes
# Commands
1. use `git log` to see details about commits

2. use `-u` or `--set-upstream` when pushing a branch for the first time to link the local branch to the remote branch, making future pushes and pulls easier, ie `git push -u origin <branch>`

3. use `git merge --abort` to abort a merge in case of a conflict

4. use `git reset --soft HEAD~n` removes the last `n` number of commits

5. use `git reset --hard HEAD~n` removes the last `n` number of commits permanently(unless we have the commit hash). ==Note: Never do this with pushed commits==

6. `git log --oneline` to display commit logs with only their hashes and the commit message. ==Note: only the first 7 characters of the hash are required==

7. `git stash` to store the current workspace to switch tasks
8. `git stash pop` to restore a stash. Note that each branch maintains its own stash. Can be verified using `git stash list`
9. `git stash list` to see the stash list
10. `git stash apply` to retrieve an item from the stash without deleting it from the stash
11. `git stash drop` to delete a stash
12. `git stash clear` to delete all stashes
13. `git stash push -m "<message>"` can be used to name the stashes for better clarity

14. `git rebase <branch>` to rebase the current branch with `branch`. Note that the commits from the current branch will appear AFTER the commits of `branch`
15. `git rebase --abort` to stop a rebase
16. `git rebase -i` to start interactive rebasing

17. `git tag -a <tag-annotation(eg, a version)> -m '<message>'` to create an annotated tag
18. `git tag` to display all tags
19. `git push origin --tags` to push all tags to the remote repository

20. `git log --graph` shows the branch structure
21. `git log --grep='<message-keyword>'` can be used to search the commit messages
22. `git log --oneline -n n` to limit to last N commits
23. use flags like `--author`, `--since`, and `--until` to filter by author or date

24. `git show <hash>` shows details about a particular commit

25. `git blame -L <start>,<end> <filepath>` to show which author wrote specific lines in a file with lines starting from `start` till `end`, inclusive