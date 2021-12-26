# Git commands

## Table of contents

- [Git configuration](#git-configuration)
  - [Standard configuration](#Standard-configuration)
  - [Setting up Personal Access Token](#Setting-up-Personal-Access-Token) 
- [Creating Snapshots](#Creating-Snapshots)
  - [Initialize a repository](#Initialize-a-repository)
  - [Staging files](#Staging-files)
  - [Git Status](#git-status)
  - [Removing files](#Removing-files) 
  - [Renaming or moving files](#Renaming-or-moving-files)
  - [Committing staged files](#Committing-stageid-files)
  - [Viewing history](#Viewing-history)
  - [Unstaging files](#Unstaging-files) 
  - [Discarding local changes](#Discarding-local-changes)
  - [Restoring an earlier version of a file](#Restoring-an-earlier-version-of-a-file)
- [Branching and Merging](#Branching-and-Merging)
  - [Managing branches](#managing-branches)
  - [Merging](#Merging)

## git configuration

### Standard configuration

- **To specify your name**

```
git config --global user.name <name>
```

- **To specify your email**

```
git config --global user.email "email@domain.com"
```

- **To configure your default editor**

```
git config --global core.editor "code --wait"
```

- **To handle your EOL** 

  - For linux and mocOS 

    ```
    git config --global core.autocrlf input
    ```
    
  - For windows
    
    ```
    git config --global core.autocrlf true
    ```

- If you want to have prune executed with every fetch operation, you can configure Git accordingly

```
git config --global fetch.prune true
```

### Setting up Personal Access Token

```
git config --global credential.helper 'store --file path/to/.my-credentials'
```

## Creating Snapshots

### Initialize a repository

```
git init
```

### Staging files
 
| Command                        | Description                 |
| ---                            | ---                         |
| `git add index.html`           | ***Stages a single file***  |
| `git add index.html style.css` | ***Stages multiple files*** |
| `git add *.css`                | ***Stages with a pattern*** |

### Git Status

| Command                        | Description                 |
| ---                            | ---                         |
| `git status`                   | ***Full status***           |
| `git status -s`                | ***Short status***          | 

### Removing files

| Command                     | Description                                           |
| ---                         | ---                                                   |
| `git rm script.js`          | ***Removes from working directory and staging area*** |
| `git rm --cached script.js` | ***Removes from staging area only***                  |

### Renaming or moving files

| Command                   | Description                              |
| ---                       | ---                                      |
| `git mv script.js app.js` | ***Move or rename a file, a directory*** |

### Committing staged files

| Command                   | Description                           |
| ---                       | ---                                   |
| `git commit -m "message"` | ***Commits with a one-line message*** |


### Viewing History

| Command             | Description                              |
| ---                 | ---                                      |
| `git log`           | ***Full history***                       |
| `git log --oneline` | ***Shows Commit message only***          |
| `git log -reverse`  | ***List the from the oldest to newest*** |

### Unstaging files

| Command                          | Description              |
| ---                              | ---                      |
| `git restore --staged script.js` | ***Unstages script.js*** |

### Discarding local changes

| Command                 | Description                                               |   
| ---                     | ---                                                       |   
| `git restore script.js` | ***Copies latest script.js commit to working directory*** |   
| `git restore .`         | ***Discards all local changes but not untracked files***  |   
| `git clean -dn`         | ***List all untracked files that get removed***           |   
| `git clean -fd`         | ***Removes all untracked files***                         |   

### Restoring an earlier version of a file

| Command                                  | Description                               |
| ---                                      | ---                                       |
| `git restore --source=HEAD~2 script.js`  | ***Restores script.js back from HEAD~2*** |


## Branching and Merging

### Managing branches

| Command                           | Description                                |
| ---                               | ---                                        |
| `git branch -a`                   | ***List all branches***                    |
| `git ls-remote`                   | ***List remote branches***                 |
| `git branch <branch>`             | ***Creates a new branch***                 |
| `git checkout <branch>`           | ***Switches to the specified branch***     |
| `git switch -C <branch>`          | ***Create a branch and switches***         |
| `git switch <branch>`             | ***Switches to specified branch***         |
| `git branch -D <branch>`          | ***Deletes specified branch locally***     |
| `git push -d origin <branch>`     | ***Removes specified branch from origin*** |

### Merging

| Command                          | Description                                               |
| ---                              | ---                                                       |
| `git merge <branch>`             | ***merges the specified branch into the current branch*** |
| `git merge --no-ff <branch>`     | ***Creates a merge commit even if FF is possible***       |


