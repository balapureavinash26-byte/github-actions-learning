# GitHub Actions Lesson 2 – First GitHub Actions Workflow

## Objective

The objective of this lesson is to create the first GitHub Actions workflow and 
understand how GitHub automatically executes a workflow whenever code is pushed 
to a GitHub repository.

This lesson demonstrates a basic Continuous Integration (CI) pipeline using GitHub 
Actions.

# What is a GitHub Actions Workflow?

A Workflow is an automated process defined in a YAML file.
It contains one or more jobs that execute automatically when a specified event occurs.

Example:-

Developer
     │
     ▼
Push Code
     │
     ▼
GitHub Actions
     │
     ▼
Run Workflow


# Workflow File Location

GitHub automatically detects workflow files stored inside:

.github/workflows/

Example:

.github/
└── workflows/
    └── hello.yml

# Workflow Trigger

This workflow is triggered whenever code is pushed to the **main** branch.

   yaml
on:
  push:
    branches:
      - main

# Runner

The workflow runs on GitHub's hosted Ubuntu virtual machine.

    yaml
runs-on: ubuntu-latest

The runner executes all the workflow steps.

# Workflow (hello.yml)

```yaml
name: My First GitHub Action

on:
  push:
    branches:
      - main

jobs:
  hello-job:
    runs-on: ubuntu-latest

    steps:

      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Print Welcome Message
        run: echo "Hello Avinash! Welcome to GitHub Actions."

      - name: Show Current Directory
        run: pwd

      - name: List Files
        run: ls -l

      - name: Show Date
        run: date

      - name: Show Current User
        run: whoami

      - name: Finish
        run: echo "Workflow Completed Successfully!"
```

# Workflow Explanation

# Workflow Name #

```
My First GitHub Action
```

The name displayed in the GitHub **Actions** tab.

# Event #

```
push
```

Starts the workflow whenever code is pushed to the **main** branch.

# Job #

```
hello-job
```
A job is a collection of steps executed on a runner.

# Steps #

The workflow performs the following steps:

- Checkout repository
- Print welcome message
- Display current directory
- List repository files
- Display current date
- Display current user
- Print completion message

# Workflow Execution Flow

```
Developer
     │
     ▼
git add
     │
     ▼
git commit
     │
     ▼
git push
     │
     ▼
GitHub detects Push Event
     │
     ▼
Creates Ubuntu Runner
     │
     ▼
Downloads Repository
     │
     ▼
Executes Workflow
     │
     ▼
Displays Result
```

# Console Output

Example output:

```
Hello Avinash! Welcome to GitHub Actions.

...

/home/runner/work/github-actions-learning

...

Workflow Completed Successfully!
```

---

# What I Learned

- Understood GitHub Actions workflow execution.
- Created my first GitHub Actions workflow.
- Learned the purpose of workflow triggers.
- Learned how GitHub-hosted runners execute workflows.
- Used `actions/checkout@v4` to download the repository.
- Executed Linux shell commands inside GitHub Actions.
- Viewed workflow logs in the GitHub Actions dashboard.

---

# Interview Questions

### 1. What is GitHub Actions?

GitHub Actions is GitHub's built-in CI/CD automation service that automates software development workflows.

---

### 2. What is a Workflow?

A Workflow is an automated process defined in a YAML file that consists of one or more jobs.

---

### 3. Where are workflow files stored?

Workflow files are stored inside:

```
.github/workflows/
```

---

### 4. What is a Runner?

A Runner is the virtual machine or computer that executes a GitHub Actions workflow.

---

### 5. What is the purpose of `actions/checkout@v4`?

It downloads the repository source code from GitHub to the runner so that the workflow can access and use the project files.

---

### 6. Which event triggered this workflow?

The **push** event on the **main** branch.

---

### 7. Which language is used to write GitHub Actions workflows?

**YAML**

---

# ✅ Result

Successfully created and executed my first GitHub Actions workflow.

The workflow automatically started when code was pushed to the **main** branch, 
executed all configured steps on a GitHub-hosted Ubuntu runner, and completed 
successfully.

This lesson provided practical experience with GitHub Actions, workflow triggers, 
runners, jobs, and steps, forming the foundation for building CI/CD pipelines.
