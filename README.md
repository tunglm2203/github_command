My note for github:
# Delete remote branch
`git push origin --delete` <branch> # Git version 1.7.0 or newer\
`git push origin :<branch>` # Git versions older than 1.7.0

# Delete a local branch
`git branch --delete <branch>`\
`git branch -d <branch>` # Shorter version\
`git branch -D <branch>` # Force delete un-merged branches

# Delete a local remote-tracking branch
`git branch --delete --remotes <remote>/<branch>`\
`git branch -dr <remote>/<branch>` # Shorter\
`git fetch <remote> --prune` # Delete multiple obsolete tracking branches\
`git fetch <remote> -p` # Shorter

# If you want to list all the files currently being tracked under the branch master, you could use this command:
`git ls-tree -r master --name-only`


# Add changed files to an old (not last) commit
1. Use `git stash` to store the changes you want to add.
2. Use `git rebase -i HEAD~10` (or however many commits back you want to see).
3. Mark the commit want to change for edit by changing the word `pick` at the start of the line into `edit`. Don't delete the other lines as that would delete the commits.
4. Save the rebase file, and git will drop back to the shell and wait for you to fix that commit.
5. Pop the stash by using `git stash pop`
6. Add your file with `git add <file>`
7. Amend the commit with `git commit --amend --no-edit`
8. Do a `git rebase --continue` which will rewrite the rest of your commits against the new one. If there are some files you didn't add, then use `git stash` before rebase. After you come back the newest commit, do `git stash pop` to return whole files
9. Repeat from step 2 onwards if you have marked more than one commit for edit.
