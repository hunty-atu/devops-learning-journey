"git pull --rebase origin" main followed by "git push origin main" fixed the issue! Here's what was happening:

Diverged Branches: Your local branch and the remote branch had diverged. This means there were new commits on the remote branch that your local branch didn't have.

Non-Fast-Forward Update: Git requires that your local branch be up-to-date with the remote branch before you can push changes. Since your local branch was behind, Git rejected the push to prevent overwriting changes on the remote branch.

Rebase Solution: By using git pull --rebase origin main, you fetched the latest changes from the remote branch and reapplied your local commits on top of these changes. This ensured that your local branch was up-to-date and included all the latest commits from the remote branch.

Successful Push: After rebasing, your local branch was aligned with the remote branch, allowing you to push your changes without any conflicts.
