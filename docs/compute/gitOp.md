---
title: Git operation
tags:
  - git
categories: programming
cover: img/hisameTop.png
---

### Branch

| Operation                    | Command                            |
| ---------------------------- | ---------------------------------- |
| create new branch            | `git branch {branch name}`         |
| check branch                 | `git branch`                       |
| switch branch                | `git switch {branch name}`         |
| delete branch                | `git branch -d {branch name}`      |
| switch and create new branch | `git switch -c {new branch name}`  |
| push branch to origin        | `git push -u origin {branch name}` |

### Commit

| Operation                         | Command                                         |
| --------------------------------- | ----------------------------------------------- |
| Commit single file                | `git commit {path_to_file} -m "commit message"` |
| commit all                        | `git commit -a -m "message`                     |
| amend commit                      | `git commit -m "message" --amend`               |
| amend commit without edit message | `git commit --amend --no-edit`                  |
| Go back to specific commit        | `git reset {commitID}`                          |

### Stash
| Operation               | Command                         |
| ----------------------- | ------------------------------- |
| stashing untracked file | `git stash --include-untracked` |
| stashing specifc file   | `git stash push {files}`        |

### Staging
| Operation | Command                        |
| --------- | ------------------------------ |
| Staging   | `git add {files}`              |
| Unstaging | `git restore --staged {files}` |

### Reset
```
git reset {commitID}
```
reset the base to certain commit and keep your own working directory

```
git reset --hard {commitID}
```
force the working directory into the certain commit, changes will not be kept
### Remove a commit / force push old commit

```
git reset --hard {commitID}
git push --force
```

### When you hard reset and lost all your changes
1. Find the lost commit id by
```
git reflog
```
2. hard reset to the commit
```
git reset --hard {lostCommitID}
```

## Edit branch name for local and remote
1. Rename the branch
```
git branch -m <old-name> <new-name>
```
2. delete the target branch in remote and re-create the upstream of it
```
git push origin --delete <old-name>
git push origin -u <new-name>
```

## Rebase
Literally take current version to compare the target and convert a commit.  Like editing start from the target