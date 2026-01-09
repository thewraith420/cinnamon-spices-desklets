# Reporting Bugs

* It's important to use a proper title when opening new issues. The title must be in the format `spice name: simple description of the problem`.

Issues that don't follow this format will be closed.

You should mention the author on GitHub by typing @ plus his/her username to trigger a notification and bring his/her attention to an issue or pull request.
You find the username of the author on the cinnamon spices website: https://cinnamon-spices.linuxmint.com/

If possible tell us
* how exactly can we reproduce the error
* what you expected to happen
* what _actually_ happened
* whether the problem happens consistently or intermittently
* the version of Cinnamon and which Linux distro you are running

# Creating Pull Requests

* It's important to use a proper title in the **commit messages and pull requests**. The title must be in the format `spice name: simple description, what the commit/pull request does`.
* One Pull Request - One Desklet. This avoids the risk of having to revert changes to multiple desklets if any problem is subsequently found with the PR.  It also means that reviewing your changes is more straightforward.

Pull Requests that don't follow this format will be closed.

You should mention the author on GitHub by typing @ plus his/her username to trigger a notification and bring his/her attention to an issue or pull request.
You find the username of the author on the cinnamon spices website: https://cinnamon-spices.linuxmint.com/

Nice to know
* You can close issues through commit/pull request messages (https://help.github.com/articles/closing-issues-via-commit-messages/)
* How to change the commit message (https://help.github.com/articles/changing-a-commit-message/)

## Cleaning Up Multiple Commits

If you have made multiple commits on your branch and want to clean them up before your pull request is merged, you can squash them into a single commit or fewer commits. This makes the project history cleaner and easier to review.

### Method 1: Interactive Rebase (Recommended)

Interactive rebase allows you to combine, reorder, and edit commits.

1. First, determine how many commits you want to squash. Check your recent commits:
   ```bash
   git log --oneline
   ```

2. Start an interactive rebase. Replace `N` with the number of commits you want to modify:
   ```bash
   git rebase -i HEAD~N
   ```
   
   For example, to modify the last 3 commits: `git rebase -i HEAD~3`

3. Your editor will open with a list of commits. Change `pick` to `squash` (or just `s`) for the commits you want to combine:
   ```
   pick abc1234 spice name: first commit
   squash def5678 spice name: second commit
   squash ghi9012 spice name: third commit
   ```
   
   The first commit should remain as `pick`, and the others should be `squash`. This will combine all commits into the first one.

4. Save and close the editor. Another editor window will open for you to edit the combined commit message.

5. Edit the commit message to follow the format: `spice name: simple description`

6. Save and close the editor.

7. Force push your changes to update your pull request:
   ```bash
   git push --force-with-lease origin your-branch-name
   ```

### Method 2: Soft Reset (Alternative)

This method is simpler but requires you to recommit everything:

1. Check your commit history to find the commit hash before your changes:
   ```bash
   git log --oneline
   ```

2. Reset to that commit while keeping your changes:
   ```bash
   git reset --soft COMMIT_HASH
   ```
   
   For example: `git reset --soft abc1234`

3. Now all your changes are staged. Commit them as a single commit:
   ```bash
   git commit -m "spice name: description of your changes"
   ```

4. Force push to update your pull request:
   ```bash
   git push --force-with-lease origin your-branch-name
   ```

### Important Notes

* Always use `--force-with-lease` instead of `--force` when force pushing. It's safer as it won't overwrite changes if someone else has pushed to your branch.
* Make sure your commit message follows the format: `spice name: simple description`
* Only rewrite history on your own branches, never on shared branches like `master`
* If you're unsure, create a backup branch first: `git branch backup-branch-name`
