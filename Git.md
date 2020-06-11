# _Git_

- https://git-scm.com/

---

# _Setup_

- https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup

* Open Git config in VSCode
  - `code $HOME/.gitconfig`
* `git config --global user.name "hmm"`
* `git config --global user.email hmmChase@users.noreply.github.com`
  - GitHub uses your commit email address to associate commits with your GitHub account
  - https://help.github.com/articles/setting-your-commit-email-address-on-github/
* `git config --global core.editor "code --wait"`

```
[user]
    email = hmmChase@users.noreply.github.com
    name = hmm
[core]
    editor = code --wait
```

- To view the version of Git installed:
  - `git --version`

---

# _Stages_

- unstaged
- stagged
- commited

---

# _init_

- Initialize git for a project
  - `git init`

---

# _config_

- View git config
  - `git config —list`

* Edit global config
  - `git config --global --edit`
  - `git config --global -e`

- Set your name:
  - `git config --global user.name "Your Name"`

* Set your email:
  - `git config --global user.email youremail@example.com`

- Add your GitHub username
  - `git config --global user.username username`

* Make VS Code default git editor
  - `git config --global core.editor "code --wait"`

## _Line endings_

- https://help.github.com/articles/dealing-with-line-endings/
- There are 3 options:
  - Checkout Windows-style, commit Unix-style:
    - Git will convert LF to CRLF when checking out text files. When committing text files, CRLF will be converted to LF. For cross-platform projects, this is the recommended setting on Windows ("core.autocrlf" is set to "true")
  - Checkout as-is, commit Unix-style:
    - Git will not perform any conversion when checking out text files. When committing text files, CRLF will be converted to LF. For cross-platform projects this is the recommended setting on Unix ("core.autocrlf" is set to "input").
  - Checkout as-is, commit as-is:
    - Git will not perform any conversions when checking out or committing text files. Choosing this option is not recommended for cross-platform projects ("core.autocrlf" is set to "false")
- To change:
  - `git config --global core.autocrlf true|false|input`

---

# _stash_

- Put in stash
  - `git stash save "Message"`

* Show stash
  - `git stash list`

- Show stash stats
  - `git stash show stash@{0}`

* Show stash changes
  - `git stash show -p stash@{0}`

- Use custom stash item and drop it
  - `git stash pop stash@{0}`

* Use custom stash item and do not drop it
  - `git stash apply stash@{0}`

- Delete custom stash item
  - `git stash drop stash@{0}`

* Delete complete stash
  - `git stash clear`

---

# _add_

- Adds files to staging

* Stage a file's changes to be committed
  - `git add <FILENAME>`

- To stage all files changes
  - `git add .`

* Update all changes
  - `git add -u`

## _--patch_

- To add changes one at a time

  - `git add --patch`
  - `git add -p`

    - `y` - Stage this hunk
    - `n` - do not stage this hunk
    - `q` - quit; do not stage this hunk or any other hunks
    - `a` - stage this hunk, and all hunks after this one
    - `d` - do not stage this hunk, or any later hunks in the file
    - `g` - select a hunk to go to
    - `/` - search for a hunk using a regex
    - `j` - leave this hunk undecided, see next undecided hunk
    - `J` - leave this hunk undecided, see next hunk
    - `k` - leave this hunk undecided, see previous undecided hunk
    - `K` - leave this hunk undecided, see previous hunk
    - `s` - split the current hunk into smaller hunks
    - `e` - manually edit the current hunk
    - `?` - print the list of commands

---

# _pull_

- Pull in changes from a remote branch
  - `git pull <REMOTENAME> <REMOTEBRANCH>`
  - `git pull origin master`
    - will pull from the remote master branch

## _--rebase_

- from feature branch

  - `git pull --rebase origin master`

- do it on your feature branch after you commit
- creates a more linear history
- places commits from feature branches into the master branch
- never rebase if someone else is working on the same branch
- rebase everytime you commit to ensure your branch always stays in front of master

* `git rebase --abort`
  - will take you back to before you did a `git pull --rebase`

---

# _push_

- Push changes
  - `git push <REMOTENAME> <LOCALBRANCH>`

* `git push origin head`
  - `head` refers to whatever branch you last commited on

## _--delete_

- Delete a remote branch
  - `git push <REMOTENAME> --delete <BRANCHNAME>`

---

# _commit_

- To create a commit
  - `git commit`

* To commit (save) the changes you've added with a short message describing the changes
  - Message should start capitalized, have no periods, with imperative mood
  - `git commit -m "Your commit message"`

- `add` and `commit` in one step
  - `git commit -am "Message"`

* Add to most recent commit and update message
  - `git commit --amend -m "New Message"`

- Make a fake commit at a specified date
  - `git commit --amend --no-edit --date="Fri Nov 6 20:00:00 2015 -0600"`

---

# _remove_

- Remove files from Git
  - `git rm`<FILENAME>``

* Untrack file from git
  - `git rm -r —cached <FILENAME>`

---

# _move_

- Move or rename files
  - `git mv index.html dir/index_new.html`

---

# _revert_

- Go back to a specific commit
  - `git revert <SHA>`

---

# _reset_

- Unstages file
- Resets to a previous commit

* Unstage (undo adds)
  - `git reset HEAD ``<FILENAME>```

- Undo latest commit
  - `git reset --soft HEAD~`

* Soft reset (move HEAD only; neither staging nor working dir is changed)

  - `git reset --soft`<SHA>``

- Mixed reset (move HEAD and change staging to match repo (does not affect working dir)

  - `git reset --mixed`<SHA>``

* Hard reset (move HEAD and change staging dir and working dir to match repo)

  - `git reset --hard`<SHA>``

---

# _branch_

- Delete a local branch
  - `git branch -d <BRANCHNAME>`

* Create a new branch
  - `git branch <BRANCHNAME>`

- List local branches
  - `git branch`

* List remote branches
  - `git branch -r`

- Rename the branch you're currently on
  - `git branch -m <NEWBRANCHNAME>`

* Rename a branch
  - `git branch -m`<BRANCHNAME> `<NEWBRANCHNAME>`
  - `git branch --move`<BRANCHNAME> `<NEWBRANCHNAME>`

- Show all completely merged branches with current branch
  - `git branch --merged`

* Delete merged branch (only possible if not HEAD)
  - `git branch -d ``<BRANCHNAME>```
  - `git branch --delete ``<BRANCHNAME>```

- Delete not merged branch
  - `git branch -D ```<BRANCHNAME>``

---

# _clean_

- Test-Delete untracked files
  - `git clean -n`

* Delete untracked files (not staging)
  - `git clean -f`

---

# _remote_

- Show remote
  - `git remote`

* Link a project to a remote repository
  - `git remote add <REMOTENAME> <URL>`
  - `git remote add origin https://github.com/hmmChase/reponame.git`

- Remove a remote repository
  - `git remote rm origin`

* Change a remote URL
  - `git remote set-url <REMOTENAME> <URL>`

- View remote connections
  - `git remote -v`

* Show remote branches
  - `git branch -r`

---

# _checkout_

- Change the branch you're working on
  - `git checkout <BRANCHNAME>`

* Create and switch to a new branch in one line
  - `git checkout -b <BRANCHNAME>`

- Undo modifications (restore files from latest commited version)
  - `git checkout -- ``<FILENAME>```

* Restore file from a custom commit (in current branch)
  - `git checkout <SHA> -- ```<FILENAME>``

---

# _merge_

- Merges content from some branch into the current branch

* Merge a branch into current branch
  - `git merge <BRANCHNAME>`

- Merge updated master into a feature branch
  - `git merge master <FEATUREBRANCH>`

* Merge to master (only if fast forward)
  - `git merge --ff-only`<BRANCHNAME>``

- Merge to master (force a new commit)
  - `git merge --no-ff`<BRANCHNAME>``

* Stop merge (in case of conflicts)
  - `git merge --abort`

---

# _status_

- Check status of changes to a repository
  - `git status`

---

# _rebase_

- To rebase the checkedout branch into the specified branch
  - `git rebase newBranch`

---

# _log_

- Show commits
  - `git log`

* Show oneline-summary of commits
  - `git log --oneline`

- Show oneline-summary of commits with full SHA-1
  - `git log --format=oneline`

* Show oneline-summary of the last three commits
  - `git log --oneline -3`

- Show only custom commits
  - `git log --author="Sven"`
  - `git log --grep="Message"`
  - `git log --until=2013-01-01`
  - `git log --since=2013-01-01`

* Show changes
  - `git log -p`

- Show stats and summary of commits
  - `git log --stat --summary`

* Show history of commits as graph
  - `git log --graph`

- Show history of commits as graph-summary
  - `git log --oneline --graph --all --decorate`

* Export/write custom log to a file
  - `git log --author=sven --all > log.txt`

---

# _diff_

- View changes to files
  - `git diff`

* Compare modified files and highlight changes only
  - `git diff --color-words index.html`

- Compare modified files within the staging area
  - `git diff --staged`

* Compare branches
  - `git diff master..branchname`

- Compare branches like above
  - `git diff --color-words master..branchname^`

* Compare commits
  - `git diff 6eb715d` `git diff 6eb715d..HEAD` `git diff 6eb715d..537a09f`

- Compare commits of file
  - `git diff 6eb715d index.html` `git diff 6eb715d..537a09f index.html`

---

# _fetch_

- Retrieves all remote branches

* See changes to the remote before you pull in
  - `git fetch --dry-run`

---

# _Git alias_

- `alias canary='open -a "Google Chrome Canary"'`
- `alias chrome='open -a "Google Chrome"'`
- `alias github='open -a "Google Chrome Canary" http://www.github.com/'`
- `alias ga="git add"`
- `alias gb="git branch"`
- `alias gd="git diff --patience --ignore-space-change"`
- `alias gh="git log --pretty=format:\"%Cgreen%h%Creset %Cblue%ad%Creset %s%C(yellow)%d%Creset %Cblue[%an]%Creset\" --graph --date=short"`
- `alias gc="git checkout"`
- `alias gcam="git commit -m"`
- `alias gmm="git merge master"`
- `alias gpom="git pull origin master"`
- `alias gs="git status"`
- `alias ls="ls -lGFh"`

---

# _Terms_

**Commits** - A snapshot of all the files in your directory. It can (when possible) compress a commit as a set of changes, or a "delta", from one version of the repository to the next. Git also maintains a history of which commits were made when.

**Branches** - Pointers to a specific commit.

**Checkout** - To switch to a different branch.

**Merging** - Combines the work from two different branches. Merging creates a special commit that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, and the set of all their parents." It will merge the specified branch into the branch that is currently checked out.

**Rebasing** - Combines branches, but in a different manner than merging. It takes a set of commits, "copies" them, and plops them down somewhere else. It can be used to make a nice linear sequence of commits. That way it would look like two commits were developed sequentially, when in reality they were developed in parallel.

**HEAD** - the symbolic name for the currently checked out commit. It's essentially what commit you're working on top of. Detaching HEAD just means attaching it to a commit instead of a branch.

**Relative Refs** - Git only requires you to specify enough characters of a commit hash until it uniquely identifies the commit. So I can type fed2 instead of fed2da64c0efc5293610bdd892f82a58e8cbc5d8.

    * Move upwards one commit at a time with ^
    * Move upwards a number of times with ~<num>

**Repository**
A repository is a collection of related items. In our case, when writing software, it is a collection of files related to a software project. You can imagine it as a project folder with all the relevant files inside of it. In fact, that's what it will look like on your computer anyways. Sometimes they're called "repos" for short.

**Commit**
Commits are core to using Git. They are the moments in which you save and describe the work you've done. They are the ticks in the timeline of your project's history.

**Remote**
When you put something on GitHub that copy lives on one of GitHub's servers. This makes it a remote repository because it is not on your computer, but on a server, "remote" and somewhere else. By pushing your local (on your computer) changes to it, you keep it up to date.

Others can always then get the latest from your project by pulling your changes down from the remote (and onto their computer). This is how everyone can work on a project together without needing access to your computer where your local copy is stored.

You can have multiple remotes so each requires a name. The primary remote is typically named “origin”.

**Push**
Send everything you've done locally to your remote repository.

---

**Pull**
Others can always then get the latest from your project by pulling your changes down from the remote.

If you're working on something with someone else, you need to stay up to date with the latest changes. So, you'll want to pull in any changes that may have been pushed to the central GitHub repository.

---

**Fork**
When you fork a repository, you're creating a copy of it on your GitHub account. Your forked copy begins its life as a remote repository—it exists just on your GitHub account, not on your computer. Forks are used for creating your own version of a project (this diversion from the original is like taking a fork in the road) or contributing back your changes (such as bug fixes or new features) to the original project.

**Clone**
To get a forked repository from your GitHub account onto your computer you clone it. This cloning action copies the remote repository onto your computer so that you can work on it locally.

**Branches**
Git repositories use branches to isolate work when needed. It's common practice when working on a project or with others on a project to create a branch to keep your working changes in. This way you can do your work while the main, commonly named 'master', branch stays stable. When the work on your branch is finished, you merge it back into the 'master' master branch.

When you create a branch, Git copies everything from the current branch you're on and places it in the branch you've requested be made.

**Pull Requests**
Often when you make changes and improvements to a project you've forked, you'll want to send those changes to the maintainer of the original and request that they pull those changes into the original so that everyone can benefit from the updates.

---

# _Workflow_

## Setting up the repository

1. Initialize a new Git repository (repo) and make initial file structure
2. Create a new repository on GitHub
3. Link your local and GitHub repository (add remote)
4. Push structure to remote repository (on the master branch)
5. Add all team members as collaborators

## Once the repository is setup, repeat this process

1. start on master
2. `git checkout -b [feature-branch-name]`
3. do work
4. commit (add, commit)
5. update local master and pull changes into your feature branch

   1. either merge
      1. `git checkout master`
      2. `git pull origin master`
      3. `git checkout [feature-branch-name]`
      4. `git merge master`
   2. or rebase (preferable)
      1. from feature branch
      2. `git pull --rebase origin master`

6. fix conflicts! (tells you on command line where to look in editor)
7. repeat until feature complete
8. run tests if applicable
9. `git push origin [feature-branch-name]`
   1. or `git push origin head`
   2. or `git push -f origin head` if needed
10. go to GitHub! (with homebrew, in the terminal, type `hub browse`)
11. create a pull request (make sure its going to the right place)
12. hit the ‘submit pull request’ button
13. contact partner to review pull request
14. partner merges pull request
15. `git checkout master`
16. `git pull origin master`
17. repeat the process

---

# _Hooks_

- http://frontend.turing.io/lessons/module-4/advanced-git-workflow.html
- Custom scripts that you can write to execute particular tasks during certain points of the git workflow process
- View them at `/.git/hooks`
- The language is bash
- By default, they are not included in commits or pushed to Github

## Lifecycles

- `pre-commit` - runs before the commit is even attempted, can be used to do a quick QA evaluation on the code that’s about to be committed
- `prepare-commit-msg` - runs before the commit message is made but after a default message is created, e.g. merge commits are auto-generated and can be adjusted at this point in the cycle
- `commit-msg` - runs after the commit message has been made, can be used to verify that your message follows a required pattern (e.g. capital first letter, no punctuation, command-style sentence)
- `post-commit` - runs after the entire commit process is completed, can be used to run another script based on information from the most recent commit

## Examples

### Pre-Commit

- Testing
  - Let’s rename `pre-commit.sample` to `pre-commit` and open it in your text editor. We’re going to create a `pre-commit` hook that prevents us from committing code that doesn’t conform to our linting and testing standards. We’re not going to use any of the example functionality that was included, so we can remove everything in this file and replace it with the following:

```
`#!/bin/sh

echo "\Running tests:\n"

npm run test --silent`
```

    * Now if we have a failing test, our pre-commit hook should catch that and prevent the commit from going through. This hook is super simple right now, because a failing test automatically causes the process to exit with an error.

- Linting
  - If we were to add linting to this hook:

```
`#!/bin/sh

echo "\Running tests:\n"

npm run test --silent
npm run lint --silent`
```

- Console.Logs/Accepting User Input
  - We might also want to check for `console.logs` or `debugger` statements in our code before committing, because embarassing things like [this](https://twitter.com/CLINT/status/493173618105274369)might happen. Sometimes (though rarely), you might actually want to include an intentional `console.log`. With the following script, we can allow users to choose whether or not to continue with the commit if any logs are detected:

```
`echo "\nChecking for console.logs()...\n"exec 1>&2# enable user inputexec < /dev/tty
consoleregexp='^\+.*console\.log('debuggerregexp='debugger'if test $(git diff --cached | grep $consoleregexp | wc -l) != 0then
  exec git diff --cached | grep -ne $consoleregexpread -p "You have added one or more console logs in your modification. Are you sure want to continue? (y/n)" yn
  echo $yn | grep ^[Yy]$if [ $? -eq 0 ]then
    exit 0; # Let the user continueelse
    exit 1; # Don't let the user continuefi
fi
if test $(git diff --cached | grep $debuggerregexp | wc -l) != 0then
  exec git diff --cached | grep -ne $debuggerregexpread -p "You have added one or more debuggers in your modification. Are you sure want to continue? (y/n)" yn
  echo $yn | grep ^[Yy]$if [ $? -eq 0 ]then
    exit 0; # Let the user continueelse
    exit 1; # Don't let the user continuefi
fi`
```

---

# _Gitignore_

- https://www.gitignore.io/

```
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Runtime data
pids
*.pid
*.seed
*.pid.lock

# Directory for instrumented libs generated by jscoverage/JSCover
lib-cov

# Coverage directory used by tools like istanbul
coverage

# nyc test coverage
.nyc_output

# Grunt intermediate storage (http://gruntjs.com/creating-plugins#storing-task-files)
.grunt

# Bower dependency directory (https://bower.io/)
bower_components

# node-waf configuration
.lock-wscript

# Compiled binary addons (https://nodejs.org/api/addons.html)
build/Release

# Dependency directories
node_modules/
jspm_packages/

# TypeScript v1 declaration files
typings/

# Optional npm cache directory
.npm

# Optional eslint cache
.eslintcache

# Optional REPL history
.node_repl_history

# Output of 'npm pack'
*.tgz

# Yarn Integrity file
.yarn-integrity

# dotenv environment variables file
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# parcel-bundler cache (https://parceljs.org/)
.cache

# next.js build output
.next

# nuxt.js build output
.nuxt

# vuepress build output
.vuepress/dist

# Serverless directories
.serverless

# production
build/

# private
private/

# misc
.DS_Store
.vscode
```

---
