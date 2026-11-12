# GIT AND GITHUB FOR CLOUD ENGINEERS

### 

A practical documentation of Git and GitHub concepts, commands, workflows, and their relevance to cloud engineering.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Understanding Git](#2-understanding-git)
3. [Git Workflow](#3-git-workflow)
4. [Branching and Merging](#4-branching-and-merging)
5. [GitHub and Remote Repositories](#5-github-and-remote-repositories)
6. [Git Fetch and Git Pull](#6-git-fetch-and-git-pull)
7. [Pull Requests](#7-pull-requests)
8. [Version Tagging](#8-version-tagging)
9. [Relevance to Cloud Engineering](#9-relevance-to-cloud-engineering)
10. [Challenges and Lessons Learned](#10-challenges-and-lessons-learned)
11. [Conclusion](#11-conclusion)
12. [Learning Resource](#12-learning-resource)

---

## 1. Introduction

Git and GitHub are important tools in software development and cloud engineering. They help developers manage changes, maintain project history, and collaborate on projects.

The purpose of this project is to understand how Git and GitHub work, practise their essential commands, and explore how version control supports cloud engineering activities such as Infrastructure as Code (IaC), automation, and deployment workflows.

### Tools Used

- Git
- Git Bash
- GitHub
- Visual Studio Code

---

## 2. Understanding Git

### What is Git?

Git is a distributed version control system that tracks changes to files and manages project history. It allows developers to record changes, revisit previous versions, and work on different branches of a project.

### What is GitHub?

GitHub is an online platform for hosting Git repositories. It allows developers to access repositories remotely, share projects, review changes, and collaborate with other developers.

### Git versus GitHub

| Git | GitHub |
|---|---|
| A version control system. | An online platform for hosting Git repositories. |
| Tracks changes and project history. | Provides remote repository hosting. |
| Can be used locally. | Provides collaboration and repository management features. |

### Why Cloud Engineers Need Git and GitHub

Cloud engineers work with infrastructure configurations, automation scripts, deployment files, and application code.

Git helps track changes made to these files, while GitHub provides a platform for hosting repositories and collaborating with other engineers.

They are particularly useful when managing Infrastructure as Code, automation, deployments, and infrastructure changes.

### Git Installation and Configuration

I first confirmed that Git was installed on my computer.

**Command:**

```bash
git --version
```

I also configured my username and email address so Git could recognise me when creating commits.

**Commands:**

```bash
git config --global user.name "Your Name"

git config --global user.email "your-email@example.com"
```

To verify the configuration:

```bash
git config --global user.name

git config --global user.email
```

### Practical Evidence

![Git version verification](screenshots/01-git-version.png)

*Figure 1: Verifying the installed Git version.*

![Git configuration](screenshots/02-git-configuration.png)

*Figure 2: Configuring the Git username and email address.*

---

## 3. Git Workflow

Git has three important areas:

1. **Working Directory:** Where you create and modify files.
2. **Staging Area:** Where you select changes to include in your next commit.
3. **Local Repository:** Where Git permanently records your commits in the project history.

The general Git workflow involves making changes, staging those changes, and committing them to the local repository.

### 3.1 Repository Initialisation

A repository is initialised using the `git init` command.

This command creates a Git repository inside the current project folder.

```bash
git init
```

![Git initialisation](screenshots/03-git-init.png)

*Figure 3: Initialising a Git repository.*

### 3.2 Staging Changes

Staging is the process of selecting changes to be included in the next commit.

To add a particular file:

```bash
git add filename
```

To stage all changes in the current directory:

```bash
git add .
```

![Git staging](screenshots/04-git-staging.png)

*Figure 4: Adding files to the staging area.*

### 3.3 Checking Repository Status

The `git status` command shows the current state of the repository.

```bash
git status
```

In my practical, the output showed that I was currently on the `master` branch and there was nothing to commit.

![Git status](screenshots/05-git-status.png)

*Figure 5: Checking the current repository status.*

### 3.4 Creating Commits

Commits are used to record staged changes in the local repository.

A commit acts as a snapshot of the project at a particular point in time, allowing the project history to be reviewed.

**Command:**

```bash
git commit -m "A brief description of what you did"
```

![Git commit](screenshots/06-git-commit.png)

*Figure 6: Creating a Git commit.*

### 3.5 Viewing Commit History

To view the commit history, use:

```bash
git log
```

To display the commit history in a shorter format:

```bash
git log --oneline
```

![Git log](screenshots/07-git-log.png)

*Figure 7: Viewing the repository's commit history.*

---

## 4. Branching and Merging

### What is a Branch?

A branch is an independent line of development. It allows developers to work on different features without immediately changing the main project.

For example, when creating infrastructure for an organisation, you may have:

- `main`: The approved version of the project.
- `development`: Where ongoing development happens.
- `feature-storage`: Where you develop a storage-related feature.
- `feature-network`: Where another engineer develops networking resources.

The purpose is to allow different development activities without immediately changing the main project.

### Branch Commands

To know which branch you are currently working on:

```bash
git branch
```

To create a branch and switch to it:

```bash
git switch -c feature-network
```

An alternative command is:

```bash
git checkout -b feature-network
```

To switch to an existing branch:

```bash
git switch main
```

### What is Merging?

Merging combines changes from one branch into another.

There are two main types of merge:

**1. Fast-forward Merge**

A fast-forward merge happens when the target branch has no new commits that diverge from the source branch. Git simply moves the target branch forward to include the commits.

**2. Three-way Merge**

A three-way merge happens when both branches have new work after they split.

Git examines three points:

- Where the branches originally split.
- Where the source branch is currently.
- Where the target branch is currently.

It combines the changes and normally creates a new merge commit to record the merge.

In my practical, I made use of the fast-forward merge.

**Merge command:**

```bash
git merge feature-network
```

![Branch creation](screenshots/08-branch-creation.png)

*Figure 8: Creating and switching between branches.*

![Fast-forward merge](screenshots/09-fast-forward-merge.png)

*Figure 9: Performing a fast-forward merge.*

### Merge Conflicts

A merge conflict occurs when Git cannot automatically combine changes between two branches.

For example, if two people modify the same line of code differently, Git may encounter a conflict when the branches are merged.

The conflicting file must be reviewed and corrected before the merge can be completed.

After resolving the conflict, the file is staged and the merge is completed with a commit.

**Commands:**

```bash
git status

git add filename

git commit -m "Resolve merge conflict"
```

![Merge conflict](screenshots/10-merge-conflict.png)

*Figure 10: Identifying a merge conflict.*

![Conflict resolution](screenshots/11-conflict-resolution.png)

*Figure 11: Resolving the merge conflict.*

---

## 5. GitHub and Remote Repositories

### What is a Remote Repository?

A remote repository is a version of your Git repository hosted somewhere outside your local machine, such as GitHub.

It allows developers to share their work and exchange changes between local and remote repositories.

### Creating and Connecting a GitHub Repository

I created a repository on GitHub, added it to my local Git repository, and pushed the contents of the `azurenetwork` branch to GitHub.

To add a GitHub repository as a remote:

```bash
git remote add origin YOUR_GITHUB_REPOSITORY_URL
```

To confirm the remote repository:

```bash
git remote -v
```

To push the contents of a branch to GitHub:

```bash
git push -u origin azurenetwork
```

![GitHub repository](screenshots/12-github-repository.png)

*Figure 12: Creating a repository on GitHub.*

![Remote configuration](screenshots/13-git-remote.png)

*Figure 13: Connecting and verifying the remote repository.*

![Git push](screenshots/14-git-push.png)

*Figure 14: Pushing the azurenetwork branch to GitHub.*

### Challenge Faced: Master and Main Branches

I noticed that when I pushed my default `master` branch from my local Git repository to GitHub, it appeared as another branch entirely on GitHub.

I decided to rename my local branch from `master` to `main`, pulled the contents of the `main` branch from GitHub into my local repository, and pushed my changes back to GitHub.

During this process, I noticed that the repository contained two README files. I later realised that I needed to manage the local and remote repository contents more carefully.

I renamed the README file in my local repository to `notes.md`.

**Commands involved:**

```bash
git branch -M main

git pull origin main

git push -u origin main
```

These commands show the branch renaming and synchronisation steps. When local and remote histories differ, Git may require additional reconciliation before the pull can complete.

![Main branch synchronisation](screenshots/15-main-branch-synchronisation.png)

*Figure 15: Synchronising the local and remote main branches.*

![Notes file](screenshots/16-notes-file.png)

*Figure 16: Renaming the local README file to notes.md.*

---

## 6. Git Fetch and Git Pull

### Git Fetch

Git Fetch retrieves changes from the remote repository and updates remote-tracking references.

It does not automatically integrate those changes into your current local branch.

**Command:**

```bash
git fetch origin
```

### Git Pull

Git Pull fetches changes from the remote repository and then integrates them into the current branch.

**Command:**

```bash
git pull origin main
```

### Practical Demonstration

In this practical, I edited my README file on GitHub and used fetch and pull to retrieve the changes and integrate them into my local Git branch.

The difference is that `git fetch` retrieves remote updates without integrating them, while `git pull` retrieves and integrates them.

![Remote README edit](screenshots/17-remote-readme-edit.png)

*Figure 17: Editing the README file on GitHub.*

![Git fetch](screenshots/18-git-fetch.png)

*Figure 18: Retrieving remote changes using Git Fetch.*

![Git pull](screenshots/19-git-pull.png)

*Figure 19: Retrieving and integrating remote changes using Git Pull.*

---

## 7. Pull Requests

### What is a Pull Request?

A pull request (PR) is a request to review and integrate changes from one branch into another.

For example, an engineer creates a feature branch, develops a storage configuration, and pushes the branch to GitHub.

They then open a pull request requesting that their changes be merged into `main`.

### Pull Request Workflow

1. Create a branch.
2. Make changes.
3. Commit the changes.
4. Push the branch to GitHub.
5. Create a pull request.
6. Request a review.
7. Receive comments or approval.
8. Address any requested changes.
9. Merge the pull request.
10. Delete the feature branch when it is no longer needed.

### Why Are Pull Requests Important?

Pull requests provide an opportunity to review infrastructure changes before they are accepted into the main codebase.

They improve accountability, collaboration, and code quality.

They also allow other engineers to examine proposed changes before those changes become part of the approved project.

### Practical Evidence

![Feature branch](screenshots/20-feature-branch.png)

*Figure 20: Creating a feature branch for development.*

![Pull request creation](screenshots/21-pull-request-created.png)

*Figure 21: Creating a pull request on GitHub.*

![Pull request review](screenshots/22-pull-request-review.png)

*Figure 22: Reviewing proposed changes.*

![Pull request merged](screenshots/23-pull-request-merged.png)

*Figure 23: Merging a pull request.*

---

## 8. Version Tagging

### What is Version Tagging?

Version tagging identifies specific points in a project's history.

Tags can be used to mark important milestones, such as project releases.

### Commands Used

To list existing tags:

```bash
git tag
```

To create an annotated tag:

```bash
git tag -a v1.0.0 -m "Initial release"
```

To push the tag to GitHub:

```bash
git push origin v1.0.0
```

### Practical Evidence

![Version tag creation](screenshots/24-version-tag-created.png)

*Figure 24: Creating the v1.0.0 version tag.*

![Version tag pushed](screenshots/25-version-tag-pushed.png)

*Figure 25: Pushing the version tag to GitHub.*

---

## 9. Relevance to Cloud Engineering

Git and GitHub are relevant to cloud engineering because cloud infrastructure involves configuration files, automation scripts, and infrastructure definitions that need to be managed and tracked.

### Infrastructure as Code (IaC)

Infrastructure as Code allows engineers to define and manage infrastructure using configuration files.

For example, Terraform uses `.tf` files to describe infrastructure resources.

These files can be stored in Git so that changes can be tracked, reviewed, and managed over time.

### Infrastructure Management

Git helps cloud engineers maintain a history of infrastructure configuration changes.

It also allows engineers to work on separate branches before merging approved changes into the main project.

### CI/CD

GitHub repositories can be connected to CI/CD pipelines to automate processes such as testing, validation, and deployment.

For example, a change pushed to GitHub can trigger an automated workflow when a pipeline has been configured.

The relationship can be represented as:

```text
Engineer makes infrastructure changes
                 |
                 v
          Git add and commit
                 |
                 v
        Push changes to GitHub
                 |
                 v
          Pull request review
                 |
                 v
         Merge approved changes
                 |
                 v
          CI/CD automation
                 |
                 v
        Cloud infrastructure
```

This project explored the relationship between Git, infrastructure management, Terraform, and CI/CD. It did not involve deploying actual Terraform infrastructure or implementing a complete CI/CD pipeline.

---

## 10. Challenges and Lessons Learned

During the practical sessions, I encountered a few challenges that helped me understand how Git works beyond simply memorising commands.

### 1. Master and Main Branch Difference

I noticed that my local repository used `master` while GitHub had a `main` branch.

I learned that branch names must be checked and managed carefully when connecting local and remote repositories.

### 2. Duplicate README Files

During the synchronisation process, I noticed that two README files appeared in the repository.

This helped me understand the importance of checking the contents and history of both local and remote repositories before pushing and pulling changes.

### 3. Understanding Remote Operations

Practising fetch and pull helped me understand that retrieving changes from a remote repository is different from integrating those changes into the current local branch.

### Lessons Learned

- Git helps developers maintain project history.
- Staging allows specific changes to be selected before committing.
- Branches support isolated development.
- Merging combines work from different branches.
- Merge conflicts require manual attention when Git cannot automatically combine changes.
- GitHub provides remote repository hosting and collaboration features.
- Pull requests support review before changes are merged.
- Version tags help identify important points in project history.
- Version control is useful for managing cloud infrastructure configurations.

---

## 11. Conclusion

Working with Git and GitHub helped me understand how developers track changes, manage project history, and collaborate through remote repositories.

The practical sessions covered repository initialisation, staging, commits, branching, merging, merge conflicts, remote repositories, pushing, fetching, pulling, pull requests, and version tagging.

I also gained a better understanding of how these tools support cloud engineering, particularly Infrastructure as Code, infrastructure management, and CI/CD workflows.

Git and GitHub are therefore important tools for cloud engineers because they provide a structured way to manage changes and collaborate on technical projects.

---

## 12. Learning Resource

The concepts and practical exercises documented in this repository were studied using the following learning resource:

**Git & GitHub for Cloud Engineers (Full Course) — Tech With Faisal**

[Watch the course on YouTube](https://www.youtube.com/watch?v=XWmH0rvLGJQ)

---

**Author:** CYB3RVIKS
**Project:** Git and GitHub for Cloud Engineers  
**Focus Area:** Cloud Engineering and Version Control
