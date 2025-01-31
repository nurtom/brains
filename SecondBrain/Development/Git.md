#git 

## Configure git user name and email

```bash
git config --global user.name "Thomas Erfurth"
git config --global user.email "t.erfurth@avidat.com"
```
## checkout remote branch

Fetch the remote branches first
```bash
git fetch
```

Optionally: Check available branches
```bash
git branch -v -a
```

Checkout remote branch (name without the remote when just on remote exists)
```bash
git switch test
```

Checkout when more than one remote exists (-c creates the new local branch)
```bash
git switch -c localbranchname origin/remotebranchname
```

## create new local branch

```bash
git checkout -b <branchname>
```

## delete local branch

```bash
git branch --delete <branchname>
```

