# GitHub Actions Lesson 5 — Job Dependencies & Outputs

## 1. Objective

The objective of this lesson was to understand how multiple GitHub Actions jobs can work 
together and how information can be passed from one job to another.In this lesson, I created
a CI pipeline with three jobs:

```text
Build → Test → Deploy

#I also practiced:

* Job dependencies
* needs:
* Step outputs
* Job outputs
* $GITHUB_OUTPUT
* Passing data between jobs
* Build → Test → Deploy workflow

# What is needs:?

The needs: keyword creates a dependency between jobs.

It tells GitHub Actions that one job must complete successfully before another job can start.

Example:

test:
  needs: build

# This means:

The Test job depends on the Build job.

Our workflow was:

Build
  ↓
Test
  ↓
Deploy

# The Test job contained:

needs: build

# The Deploy job contained:

needs: test

Therefore:

Build ✅
   ↓
Test ✅
   ↓
Deploy ✅

# What are Job Outputs?

A job output is information produced by one job that can be used by another job.
In this lesson, the Build job generated an application version.

Example:
outputs:
  version: ${{ steps.build-info.outputs.version }}

# What are Step Outputs?

A step output is information produced by a particular step.
Our Build job contained this step:

- name: Generate Build Version
  id: build-info
