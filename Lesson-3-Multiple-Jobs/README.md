# GitHub Actions – Lesson 3: Multiple Jobs and Workflow Events

## Objective

The objective of this lesson is to understand how GitHub Actions can run multiple jobs in
a CI workflow and how jobs can depend on each other.
In this lesson, I created a workflow containing three jobs:

- Build
- Test
- Deploy

I also practiced different workflow events:

- push
- pull_request
- workflow_dispatch

## What is a Job?

A Job is a group of steps that GitHub Actions executes on a runner.

Example:

```yaml
build:
  runs-on: ubuntu-latest
