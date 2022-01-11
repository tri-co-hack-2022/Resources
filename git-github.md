---
title: Git & GitHub
---

# Introduction to Git and Github 

View [workshop slides](https://alicemcgrath.digital.brynmawr.edu/pres/git-hack.html)

## Outline 

1. What are Git and GitHub? Why are they useful?
2. An introduction to GitHub and how to use it for collaboration
3. Git version control commands and workflows
4. Instructions for using the Hackathon GitHub template
5. Quick overview of Markdown

## Basics 


### Git

- [Git](https://git-scm.com/) - open-source software for version control
- Git keeps track of file changes and enables you to label them and preserve multiple version histories of a project
- Why use it?
  - Avoid file conflicts! Other collaboration/syncing tools are not designed for code
  - It helps you test code, troubleshoot, or 'undo' changes
  - Be intentional: package your changes logically, document and explain your work

### [GitHub](https://www.github.com) 

- A popular code repository for sharing and collaborating: it hosts code and enables users to manage collaboration on projects (using Git for version control).
- Why use it?
  - Widely used to develop and share open-source tools and datasets
  - Free web hosting with static site builder ([GitHub Pages](https://pages.github.com/))
  - Makes collaboration visible and transparent
  - It's what we're using to share and preserve your hackathon projects!


## Versioning vocabulary

**Repo or repository** (n.) 
: A discrete project on GitHub that contains a set of files, a change history, and a set of contributors. (E.g. [this one](https://github.com/tri-co-hack-2022/repo-template))

**Fork** (v.)
: To copy a repo's files and version history to a new one with its own settings (preserves connection with original repo but doesn't interfere). 

**Local** (adj.)
: On your computer.

**Remote** (adj.)
: On someone else's computer (aka 'the cloud').

**Clone** (v.)
: To download a local copy of a repo on GitHub with a tracked connection to the remote repo.

**Branch** (n.)
: A version of a repository with its own history. Branches can be created for a unique set of changes and later *merged* with the main branch to avoid file conflicts.

**Commit** (n.)
: A discrete set of changes to a repository that a user packages and labels.

## Getting Started with Git and GitHub

### Setting up Git on your local machine

Options:

- Install a GUI Client such as [GitHub desktop](https://desktop.github.com/) *recommended*

- [Install Git](https://git-scm.com/downloads) to use it from the command line and/or

  use Git/GitHub features for [VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#:~:text=Visual%20Studio%20Code%20has%20integrated,on%20the%20VS%20Code%20Marketplace.) or another text editor

### Setting up a repo on github

1. Sign in to your GitHub account
2. Create a new repository, import one from your computer, or **fork** one already on GitHub
3. Add recommended files: a ReadMe for documentation, a license (optional), and a .gitignore
4. **Clone** the repository to your computer
5. Open your **local** copy in VSCode or another text editor
6. Save your work often and use Git to track the changes

### Git process and commands

#### add

`git add newfile.md`

After you create a new file or save changes, tell git to track the file (also called 'staging')

NB: this stage is implicit in GitHub Desktop and on GitHub, but it's important on the command line.

#### commit 

`git commit -m "message describing my changes"`

Package your staged changes and label them for others' awareness

#### pull

`git pull`  

Update your local repo with any changes that have been committed to the remote repo

#### push

`git push origin main`

Send your changes to the remote repository and publish them on GitHub

#### Other commands 

- `git status` - see if you have staged changes
- `git branch branchname` - create a new branch
- `git checkout branchname` - switch to another branch

### Branching [workflow](https://docs.github.com/en/get-started/quickstart/github-flow)

Avoid file conflicts by working on your own branch 
![github branching diagram](https://docs.github.com/assets/cb-42360/images/help/repository/branching.png)

1. Create a branch 
2. Make changes: add, commit, push, repeat
3. Make a pull request: discuss and review your commits
4. Resolve conflicts & merge pull request 
5. Delete branch
   

### Using the Hackathon template

1. Have one team member **fork** the [Hackathon repo template](https://github.com/tri-co-hack-2022/repo-template) and invite the rest of your teammates as collaborators
2. Edit the README.md file with your team's information using markdown
3. Collaborate!
4. Share your repository link with the Hack-a-thon organizers


## [Markdown](https://www.markdownguide.org/)

- [Markdown](https://www.markdownguide.org/) - a lightweight, human-readable markup language: it encodes information in plain-text to be machine readable
- Why use it?
  - Platform-agnostic create simple rich text markup with any text editor
  - Easily human-readable compared to other markup languages (html)
  - Can be converted into any kind of document (more lightweight and sustainable than word processors)
  - It's used for documentation on GitHub 

### Syntax

```
# First level heading 

## Second-level heading

Paragraph with **bold** text and *italicized* text. 

[This is linked text](www.myurl.com)

![alt text for an image](imageurl.jpg)

```

See this [guide](https://www.markdownguide.org/cheat-sheet/) for more 

## Resources
- Git
  - Git command line [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)
  - [GitHub Desktop](https://desktop.github.com/), a GUI client for Git
  - Git features in [VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#:~:text=Visual%20Studio%20Code%20has%20integrated,on%20the%20VS%20Code%20Marketplace.)
- GitHub
  - [GitHub collaboration workflow](https://guides.github.com/introduction/flow/)
  - [GitHub & GitHub Pages tutorial](https://lab.github.com/githubtraining/introduction-to-github)
- Markdown [syntax cheatsheet](https://www.markdownguide.org/cheat-sheet/)

Content by Alice McGrath and licensed [cc-by-nc-sa](https://creativecommons.org/licenses/by-nc-sa/2.0/)