# divergent branches

Local branch and the remote branch have diverged. This means there are commits in both the local and remote branches that haven't been merged yet, and Git needs to know how to reconcile these differences.

You can resolve this by choosing a merge strategy. The options given in the hint are:

1. **Merge (Default)**:
   This is the default behavior if you want Git to merge the remote changes with your local changes.
   - Run the following command to merge:

```bash
git config pull.rebase false
```

- After this, you can do a normal pull again:

```bash
git pull origin <remote-branch>
```

2. **Rebase**:
   Rebase will apply your local commits on top of the fetched remote commits, giving a linear history.

- To set it to rebase by default, run:

```bash
git config pull.rebase true
```

- Then, do the pull again:

```bash
git pull origin <remote-branch>
```

3. **Fast-forward only**:
   If you only want to update your local branch if the remote branch is ahead and there are no divergent commits (i.e., your local branch must be behind the remote), you can set it to **fast-forward only**:

- Run:

```bash
git config pull.ff only
```

- Then, try pulling again:

```bash
git pull origin <remote-branch>
```

### To handle it once without changing your global settings:

If you want to make this decision for just this single pull without changing the default settings, you can do the following:

- **For merge** (default merge behavior):

```bash
git pull --no-rebase origin <remote-branch>
```

- **For rebase**:

```bash
git pull --rebase origin branch_mansi
```

- **For fast-forward only**:

```bash
git pull --ff-only origin branch_mansi
```
