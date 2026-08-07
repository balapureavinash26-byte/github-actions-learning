
# GitHub Actions - Introduction

## Objective

The objective of this lesson is to understand the basic concepts of GitHub Actions and how it 
automates software development workflows.

# What is GitHub Actions?

GitHub Actions is a Continuous Integration and Continuous Delivery (CI/CD) service built into 
GitHub.

It helps automate software development tasks such as:

- Building applications
- Running tests
- Deploying applications
- Sending notifications

without requiring a separate automation server.

# Why GitHub Actions?

Companies use GitHub Actions because it:

- Is built directly into GitHub
- Does not require installing Jenkins
- Supports CI/CD automation
- Uses simple YAML workflow files
- Integrates easily with GitHub repositories

# Real Workflow

```
Developer
     │
     ▼
Push Code to GitHub
     │
     ▼
GitHub Actions
     │
     ▼
Checkout Code
     │
     ▼
Build
     │
     ▼
Test
     │
     ▼
Deploy
```

# hat is a Workflow?

A Workflow is an automated process that performs one or more tasks.

Example:

```
Push Code
     │
     ▼
Run Build
     │
     ▼
Run Tests
     │
     ▼
Deploy
```

Workflow files are stored inside:

```
.github/workflows/
```

# What is an Event?

An Event tells GitHub when to start a workflow.

Examples:

- Push
- Pull Request
- Schedule
- Manual Run

Example:

```
Developer Pushes Code
        │
        ▼
Workflow Starts
```

# What is a Job?

A Job is a collection of related steps that run on a runner.

Example:

```
Job

↓

Checkout Code

↓

Build

↓

Test
```

# What is a Step?

A Step is a single task inside a job.

Examples:

- Print a message
- Run a shell command
- Build an application
- Execute tests

# What is a Runner?

A Runner is the machine that executes a GitHub Actions workflow.

GitHub provides hosted runners such as:

- Ubuntu
- Windows
- macOS

Example:

```yaml
runs-on: ubuntu-latest
```

# What is YAML?

YAML is a human-readable configuration language used to define GitHub Actions workflows.

Example:

```yaml
name: My First Workflow

on: push

jobs:
  hello:
    runs-on: ubuntu-latest
```

# enkins vs GitHub Actions

| Jenkins                    | GitHub Actions                           |
|----------------------------|----------------------------------        |
| Requires a separate server | Built into GitHub                        |
| Needs installation         | No installation                          |
| Plugin-based               | Most features built-in                   |
| More maintenance           | Less maintenance                         |
| Widely used in enterprises | Popular for modern cloud-native projects |

# What I Learned

- Understood GitHub Actions.
- Learned the purpose of Workflows.
- Learned Events, Jobs, Steps, and Runners.
- Learned that workflows are written in YAML.
- Compared GitHub Actions with Jenkins.
- Understood the basic CI/CD workflow.



