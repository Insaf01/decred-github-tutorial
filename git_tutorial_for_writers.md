# GitHub guide/tutorial for writers

## How Git is different from GitHub

GitHub is a US-based cloud service build around Git. GitHub hosts Git repositories and adds some workflow tools to it, like web view, pull requests (no such concept in Git), issues, wiki.

GitHub UI is nice, it allows us to engage more people with Git workflow, which has some outstanding fundamental properties but is hard on the UX surface

Git is the core. It is a system to track versions of files; they call it "content tracker". It is fully open source, has huge community and adoption, and was built to organize the evolution of Linux kernel source code. For the user, Git is an open source program that you can install and run locally on your device, to track versions of files.

## Getting started
How to style text with Markdown (or other "lightweight markup"), how to save changes (commit), add files, and when >1 people, how to collaborate with pull requests

To start Git book is a good read https://git-scm.com/book. This site also has a nice list of GUI clients, and a reference manual (more detailed, hardcore read for every git command).

The markdown cheatsheet to help you edit your texts:

* [markdown cheatsheet 1](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [markdown cheatsheet 2](https://guides.github.com/features/mastering-markdown/)


## Fundamentals mechanics of Git to use:

* github web UI to read PRs, review PRs, comment
* GUI tools like gitk (Linux) to browse history
* command line tools to create commits, edit history, download and upload commits (fetch and push)
* GUI tools like Meld to view diffs locally
* local text editors to edit Markdown files

## Local text editors for markdown:

* [Sublime Text](https://www.sublimetext.com/3)
* [Typora iirc](https://typora.io/)
* [Webstorm](https://www.jetbrains.com/webstorm/)
* [Visual Studio Code](https://code.visualstudio.com/)
* [brackets](http://brackets.io/)

## How to use gist:

gist is a single versioned document without collaboration tools, it's the simplest way to use git via github.

1. Open https://gist.github.com/
2. Enter short description
3. Enter file name with .md extension e.g. events-budget.md
4. Enter text
5. Click Create secret gist

It can also include multiple files. But most popular use case is single file. Later, as you edit gist all revisions will be saved in Revisions tab.
When you need collaborators it can be converted to full blown github repo with issues and pull requests.

## committing best practices advices

 The best practice is to verify yourself before two key actions: 
1) before you commit, 2) before you push

I do `git diff` and `git difftool` before the commit, the former prints diff in the command line, the latter starts my GUI diff tool (Meld).

Checking the diff before commit is doable in most GUI clients, I'm just using CLI as the international git language.

To check what I push, I do git fetch (to grab all recent commits) and git status to see if my local branch diverged from remote.

### The workflow I recommend for documents with >1 contributors is:

* when I start my work day I first check for new commits, often using web UI: https://github.com/xaur/decred-news/commits/draft11/journal/201811.md
* if there are new commits, I integrate first to reduce the amount of conflicts I'll need to resolve. First I do `git fetch` to grab all new remote commits. Then it depends:
1. if I had no unpublished local commits I just do git merge, which results in "fast forward merge" -- my local branch is advanced to the state of remote, no new (merge) commits are made)
2. if I did have unpublished local commits, I rebase them, and if they don't rebase cleanly I resolve the conflicts
* when done with integration, I add my changes and commit them
* if I anticipate other people to also author changes in parallel, I try to push more often
* this happens closer to release of the journal

### re-proper way to recover from a bad commit:

If you have not pushed it yet, `git reset --hard <commit>` is what I use to throw away bad commits. Note this also resets your working directory with any uncommitted changes to the files

If you have pushed it:

* if not too much time has passed, if not too many people fetched them, and if there are no commits on top of your bad commits, you can force-push the remote branch to a previous commit
* if any of the above is false, push a new commit that reverts the changes. Ideally, the reverting commit does nothing more than revert unwanted changes.

`<commit>` identifies the last good commit you want to reset to, can be part of the hash like `eab371`, a branch name or a tag name.

and here's a link for committing best practices in dcrd: https://github.com/decred/dcrd/blob/master/docs/code_contribution_guidelines.md#ModelGitCommitMessages

## Create an account on GitHub:

To create a new account on GitHub, you can follow these steps:

1. Create personal account: Enter your username, email, a password, and click on create an account.

2. Choose your personal plan

3. Verify your email to activate your account.

## Creating a Repository on GitHub

To create a new repository on GitHub this site https://help.github.com/en/articles/create-a-repo is a good help.

## How to create a repository with git

* After installing git, create a directory to contain the project. Go into the new directory and type git init. `git init` creates a brand new repository with its own history. If you git init in directory A, then go to directory B and run git init in B, they become two different, unrelated repositories
* Write something.
* Type `git add` to add the files.
* Type `git commit -m`.

 At this point, you have a Git repository with tracked files and an initial commit.
 
 Your local repository includes:
 
* the store of commits -- all snapshots of the directory tree known to this repo
* branches and tags assigned to the 
* a "staging area", also called an "index", a place where you prepare new commits
* a working directory where you play with files before moving them to staging area, or where you expand a given commit into.

## Editing files in your repository

To edit a file in your repository you can see this link: https://help.github.com/en/articles/editing-files-in-your-repository

## What's the best way to start a private repository to track events and spending?

To create new private repo choose Private here https://github.com/new
GitHub allows that since jan: https://github.blog/2019-01-07-new-year-new-github/

## Publishing with GitHub Pages

Publishing a website or software documentation with GitHub Pages now requires far small steps. The publishing system is called GitHub pages, and it can publish the markdown in your repository

* Create a repository (or navigate to an existing repository)
* Commit a Markdown file via the web interface, just like you would any other file
* Activate GitHub Pages via your repository’s settings
* Set it to publish from 'master' branch
* If you need home page, add index.md file at the root, the UI should show where exactly it is published
* If you need basic customizations you add _config.yml file, and if more is needed you can search a theme you like.

The UI should show where exactly it is published

## Creating a draft branche on your repository on GitHub

To create a new branch named <draft> on GitHub you can follow these steps:

* On GitHub, navigate to the main page of the repository.
* Click the branch selector menu.
* Type a new name for your new branch, for example <draft01>, then select Create branch.

## Creating a new branch named <draft> with git

Before you start working on a new document, you create the draft branch with a short name explaining the document, switch to it and place the new document there
then while the work/polishing is ongoing you commit all the intermediate states of the document to that draft branch.

one inconvenience of this workflow: the draft is only in one branch, but not in master, so if you need to edit documents in both you need to switch between them.

To create new branch you need to choose which commit use as a starting point to initialize the new branchopen your git CLI.
 
* So at first, you should execute the command in the repository directory, typing `cd <repository_name>`.
* You can create the new branch typing: `git checkout -b draft01 master`, this will create new branch named draft01 and initialize it with what master currently points at that command creates and switches to new branch in one action.
* Then you push the new branch to github git push origin draft01 -u, the -u at the end sets up an association between github's and your copy of the branch.

## Creating a pull request PR on GitHub

If you don't have write access to the repository where you'd like to create a pull request, you must create a fork, or copy, of the repository first.

This link has a detailed informations on how to create a pull request from scratch on GitHub: https://help.github.com/en/articles/creating-a-pull-request.

To make a PR, you make a new branch e.g. "polish_governance", add some commits to it and push it to your fork. Then you open a PR from that branch to upstream. Then I take those commits and do whatever I want with them to integrate them. Then you can nuke that branch locally and in your fork. Then you do git fetch for the main (draft11 in our case) branch and it updates cleanly with a fast forward git merge. Then you git push draft11 and it pushes cleanly to your fork without -f.
It pushes cleanly because no history rewriting took place on it, it happened on the temporary feature branch that you no longer care about

## How to review and edit a pull request

To review a PR, click on the files changed tab on the GitHub Web UI, this tells you what files have changed.

You’ll come to a page with two sets of the artcile: Your artcile, and the one who has been changed on the PR.

After reviewing the the pull request, you can comment on it, approve it and merge it.

## The role of `git fetch`:

The best way to "integrate remote changes" is to use `git fetch`, `git fetch` Download objects and refs from another repository

`git fetch` asks the remote about the state of its branches, and saves them in a special kind of your local branches, so-called "remote tracking branches". They are completely separate from your normal "local branches".
You can see all branches with `git branch -av`.

`git fetch` will download all commits from the remote that you don't have locally. Unlike `git pull`, `git fetch` does not do anything extra after it downloads the commits.
Hence it almost never breaks stuff or generates unwanted merge commits

The ones starting with remotes/origin/ are the "remote tracking branches". They literally track the branches of the remote 'origin'. These are the only branches that get updated with `git fetch`. Your local branches are untouched.

The power of git fetch is that after you downloaded new commits you can choose how to integrate. Maybe you want a merge, maybe you want a rebase, maybe you want a reset

## The role of `git push`

`git-push` - Update remote refs along with associated objects

For git push the full form includes remote and branch you're pushing to. For setting the upstream you, the full form is `git branch --set-upstream-to=origin/master`
All full form arguments starting with -- have short versions starting with -
You can look it up any moment with man git branch

Git tracks all directories under the root directory
If you intend to have 1 repository, you can grow any directory structure inside it. You can just deleted the .git directories, except the root one.

## The role of `git reflog`

`git reflog` Reflog allows you to go back to commits even though they are not referenced by any branch or tag. After rewriting history, the reflog contains information about the old state of branches and allows you to go back to that state if necessary.

It's an advanced command that helps you recover when things go really, really bad.

## The role of `git merge`

`git merge` is a command used to get the files from the local repository into the working directory. It incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch.

## The role of `git commit`

`git commit` is a command used to add all files that are staged to the local repository. It creates a new commit containing the current contents of the index and the given log message describing the changes.

## The role of `git pull`

`git pull` is command used to get files from the remote repository directly into the working directory. It is equivalent to a git fetch and a git merge .

## The role of `git checkout`

`git checkout` updates files in the working tree to match the version in the index or the specified tree.

"checkout" means "set my working directory to the state of commit X". Checkout your working directory with files of that branch, no extra merging step.

checkout is switching your working directory to a specified commit, most commonly used with branches, i.e. it switches to the latest commit pointed by that branch: `git checkout featurebranch1`.

Checkout is the act of unpacking a commit into a working directory. Normally you checkout a branch or a tag. A scary "detached HEAD" is when you checkout a commit without specifying a branch. Git calls it "detached" because it does not know which branch it is attached to.

## The role of `git rebase`

rebase is used to apply a set of commits on a new base commit. The best way to re-base your work on top of recent upstream updates is to do 'git rebase'.

`git rebase remote/branch` takes your current checked out branch, find which commits you have in it that are not present in remote, and tries to apply them on top of the remote branch.

first it "resets" the working directory to the state of latest commit in `remote/branch` (that's how you "get the recent files"), and then it applies changes in your local commits on top (that's how you "integrate")

## The role of `git log --oneline`

`git log --oneline` This command lists one commit per line, shows the first 7 characters of the commit SHA and the commit message.

## The role of `git remote -v`

We use it to check where we push to

## Print current branch tip

To print current branch tip, you can type `git show -s HEAD` or even better, `git log --oneline`.

## How do I now check which repo is ahead and needs to be either fetched or pushed to sync?

In the repo, you do git fetch to grab all new commits. If any, then you check git status. If your current branch is behind the remote, it will say so.

## How to reset local commits

Reset is dangerous, you throw away all local commits and force you local branch to the remote branch.
What you can use is rebase: It applies all the commits you made offline, one by one, on top of the latest remote.
If there are just a few commits `git cherry-pick` does the job, it is like rebase for single commits.

## I have an updates remote that I pushed commits to from machine A. I then want/need to switch to a different machine so I do a `git fetch` and...?

Simplest case is when you had no commits on machine B that diverged from the upstream. Then you do git merge as they advise.
Then the simplest, so called "fast forward" merge happens. It is when the local branch tip on machine B just moves forward to the latest upstream commit, with no conflicts.

more complex case when you made commits on B that diverge from A and the upstream. Then you need to "integrate" (unofficial term). There are options here. You either cherry-pick couple commits, or rebase a bunch of commits, or merge (full merge, not fast forward one, full merge includes an extra merge commit). Worst case is when you need to resolve conflicts.

For more detailed informations, you can visit this link: https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

## How to add footnotes to GitHub-flavoured Markdown?

You can visit this links, for informations about how add footnotes:

* [link 1](https://stackoverflow.com/questions/25579868/how-to-add-footnotes-to-github-flavoured-markdown)
* [link 2](https://meta.stackexchange.com/questions/5017/markdown-footnotes)

Or you can turn the [1] link into regular text by escaping markdown syntax: \[1\], and then adding links at bottom in a way that is not interpreted as links, e.g. \[id\] [text](url)
This has downsides as no autolinking (user can't click and jump).

##  what would be the best way to keep the fork remote in sync with the original over the CLI?

The data flows as origin -> your local repo -> your fork. First I run git fetch origin and inspect the commits with git log or GUI tools. If I have unpushed commits I rebase on top of latest origin (I also call it upstream sometimes). Then I add or change any further commits. Then I push to my fork git push myforkname. Then I open a PR.

## 

1. fetch upstream
2. update your local branch: there are multiple ways to update your local branch. my favorite is git merge --ff-only upstream/draft11 or git reset upstream/draft11
above two commands assume you have no extra work in your local branch and are on some older state of it
some people do git pull as advised by guides, but it may merge from upstream, which is bad
3. work on the file
4. fetch upstream (fetch upstream = fetch "from" upstream = download commits from upstream to your local repo) again and rebase in case any changes on upstream
5. push from local to origin
6. PR origin to upstream

## Informations about emails in commits

As some of you know, Git embeds the configured email address (and timezone, but that's another story) into every commit you make. For some it's okay while for some it's a privacy concern.

Once such commit is pushed, fundamentally it becomes public forever because it is posted to github event streams, that many entities are monitoring.

There was even a ghtorrent project where you could download a lot of interesting github data via a large torrent download. It allowed to lookup people's emails by their github account.

It makes more sense for large projects with many contributors, like Linux kernel (that triggered the creation of Git itself).

Second benefit of having real email address in commits I imagine is account linking. If the repository is moved from GitHub to GitLab or other system, and you add that email to your account, the commits will be linked to your profile.

The downside is the privacy leak. GitHub offers an option here to use a fake github email e.g. user@users.noreply.github.com
This way you can hide your real email while commit linking to your profile will still work.
Recently GitHub added a bit of complexity and the emails are now like 35192837+user@users.noreply.github.com.
The numeric ID is your permanent GitHub ID, it allows you to change GitHub username and still have commits properly linked to your profile.
The downside is these emails are GitHub specific and will not work if the repo is moved to another hosting.
There are many people on the web that can afford having their email address public, so not everyone necessarily will choose to hide their email. 
To enable fake github emails you need to change two places. First is GitHub settings for commits made via web UI https://github.com/settings/emails. Second is your local config.
GitHub also offers extra privacy feature on the same page "Block command line pushes that expose my email".

## How to work with two machines on github

First, if you only need a hosting between your machines, in case you want it private you either need to buy a github plan or use a hosting that offers free private repos, like bitbucket or gitlab.
If you're okay with having all the intermediate work public then ignore that.

Second, if you are the only contributor to the remote repo (from your 2 machines), you should never have any conflicts or difficult integration situations. You should always be fine even with git pull, although I recommend always forcing fast forward merges. git pull --ff-only is a short hand for git fetch followed by git merge --ff-only, which is the good thing. You can make an alias e.g. git puff (lol) and always use that, it will abort if there is an (unexpected) divergence between your local and remote branches.

Your local repository includes:

the store of commits -- all snapshots of the directory tree known to this repo
branches and tags assigned to the commits
a "staging area", also called an "index", a place where you prepare new commits
a working directory where you play with files before moving them to staging area, or where you expand a given commit into
first you "unpack" files from a certain commit into a working directory. Then you work on files, and include some, or all changes into the "staging area". When you finally make a commit, the "staged" state of the directory tree, along with commit message, timestamp and a hash, become a new commit. If you were on a branch, that branch is advanced from current top commit to the one you just made.

## What to do when I want to update my working directory to contain the most up-to-date version of my docs?

If you're the only one working on the it gets much simpler: fetch and try a fast forward merge, if that fails for some reason, then you can start thinking

That's why I suggest `git puff` as an alias for `git pull --ff-only`(git pull --ff-only is a combination of git fetch and git merge --ff-only): the fast forward merge would only fail if you make a commit on machine A and push, make another commit on machine B, then on B fetch and try to merge.

## How to clean up my working directory?

If wrong files are not committed, just move them to other place.

If git status complains it means they were committed earlier. If so, you need to commit the deletion.

Note that once you commit something, unless you don't delete or rewrite the branch it will stay forever even if you "delete" it in the following commit.

By stay forever I mean it will occupy storage space so that the commit where it was present can be checked out.

## How to update my local baranch?

Your local branch is only updated when you are switched to it and to something like git pull. If you have multiple branches, `git pull` will only update the one you are on currently. When you do `git fetch` (which is included in `git pull` too), git updates all so-called "remote tracking branches".

These are local branches in your local repo which track the state of remote (github) branches. They are special kind of branches managed by git, you don't manipulate them directly. Just `git branch` does not show them, but `git branch -a` does.

There are two helpful verbosity options you can add, `-v` and `-vv` that also show the commit hash of each branch, and the name of the remote branch a given local branch tracks

## How do I get a branch not on my local to local from github?

You can check what branches there are with `git branch -a` and then switch to it using `git checkout branchname`.

There's  also a shortcut in git: if you have a remote/x branch that has no corresponding local branch, `git checkout x` will find it, create a new branch named x and set up an association with remote/x.

## How to push directly to the upstream branch

You can use the command `git push nameofremote nameofbranch`

## How Git workflow with release branches and tags

You can find informations about it here: https://riot.im/app/#/room/#dev:decred.org/$1545436477446poOuh:decred.org
## how diffs work

there are 3 diff modes: Unified, Split and Rich Diff

you can get the Rich Diff by clicking on the <> button. It's to the right from the <> button.

You can use diff program (Meld) by installing it on your computer.

## How to write an article with RTL encoding on GitHub

To start, you can use gedit or Notepad++ as text editors.

Change file extension to .md so github recognizes it as Markdown and renders correctly

To post an article on https://gist.github.com/, you need to add `<div dir="rtl">` at the head of your article and `</div>` at the end of the article.

you can use diff program (Meld)to view the diff on the article, cause it ignores the div/rtl hack, it somehow detects text direction from the text itself
this means that it is possible to use these powerful tools with RTL text, although at the cost of more complexity for the user (need to install and configure the program)
diff program (Meld) program only shows difference between two files, it is useful by itself, but is more useful when integrated with git.


On GitHub, we need to customize the theme that renders it. GitHub Pages is based on Jekyll, so to customize the theme we need to customize a Jekyll theme: https://help.github.com/en/articles/customizing-css-and-html-in-your-jekyll-theme

There are two places to tweak: either CSS file (easy) or the template file (more complex). This is The CSS we use for RTL articles https://github.com/Insaf01/decred-journal-ar/blob/master/assets/css/style.scss

How Jekyll (static site builder) works: it takes your markdown, renders it as HTML and inserts it inside of the theme template, then the browser loads that page and applies the theme css file on top

Some hacks for the RTL to work on the article:

* For the links to work it should be written like this: arabic text [link](url).
* When we have a name in english followed by a link, it should be rewritten from `english text ([link](url))` to `english text (arabic text[link](url)`.
* For the nickname we should add the '@' or '#' after the nickname, so it can shows properly.
* the percentage mark '%' should come afeter the number
* the '-' and '+' signs should be written after the number
* It exists 3 different characters for comma: [Comma](https://unicode-table.com/en/002C/), [Arabic Comma](https://unicode-table.com/en/060C/), [Arabic Letter Waw](https://unicode-table.com/en/0648/)

