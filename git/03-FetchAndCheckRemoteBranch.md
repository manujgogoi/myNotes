# Fetch and Check remote branch locally

## Step 1: Fetch All Remote Branches

Since remote branch is not available locally, you needs to fetch it first.

```bash
git fetch origin
```

This updates the local Git repo with all remote branches.

## Step 2: Check Out Remote Branch

Now, you can create a local copy of **remote branch** from the remote repository:

```bash
git checkout -b remote_branch origin/remote_branch
```

This:

- Creates a new local branch `remote_branch`
- Tracks the remote branch `origin/remote_branch`

## Step 3: Verify the Branch Exists Locally

```bash
git branch
git branch -r # If you wants to see remote branches:
```

## Step 4: Pull Latest Updates (Optional)

To ensure the local branch is up-to-date with remote:

```bash
git pull origin remote_branch
```

## Alternative: Checkout Directly (Git 2.23+)

```bash
git switch --track origin/mansi
```

This automatically sets up tracking.
