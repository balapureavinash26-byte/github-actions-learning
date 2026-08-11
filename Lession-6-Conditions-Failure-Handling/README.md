# GitHub Actions Lesson 6 — Conditions & Failure Handling

## 1. Objective

The objective of this lesson was to understand how GitHub Actions can control workflow execution based
on success or failure.
In this lesson, I learned and practiced:

- `if:`
- `success()`
- `failure()`
- `always()`
- Job dependencies using `needs:`
- Failure handling
- Cleanup after workflow execution
- Intentional pipeline failure testing

The pipeline was tested in both successful and failure scenarios.


# 2. What is a Condition in GitHub Actions?

A condition controls whether a particular step or job should run.
GitHub Actions uses the `if:` keyword to define conditions.

Example:

```yaml
if: success()

# Important GitHub Actions Expressions #

| Expression  | Purpose                               |
| ----------- | ------------------------------------- |
| `if:`       | Defines a condition                   |
| `success()` | Runs when previous execution succeeds |
| `failure()` | Runs when something fails             |
| `always()`  | Runs regardless of success or failure |
| `needs:`    | Creates a dependency between jobs     |

---------------------------------------------------------
Q1. What is if: in GitHub Actions?

if: is used to conditionally execute a job or step.

Example:

if: success()

Q2. What is success()?

success() returns true when previous steps or jobs have completed successfully.

Q3. What is failure()?

failure() returns true when a previous step or job has failed.
It can be used for failure handling and notifications.

Q4. What is always()?

always() allows a step or job to execute regardless of whether the previous execution succeeded or failed.
It is commonly useful for cleanup activities.

Q5. What happens when a job using needs: fails?

Dependent jobs normally do not run.

Example:

Build ❌
   ↓
Test ⏭️
   ↓
Deploy ⏭️

Q6. How would you handle a failed deployment?

I would use failure-handling conditions to perform activities such as:
Sending notifications
Collecting logs
Recording failure information
Triggering troubleshooting processes
Cleaning temporary resources

Q7. What is the difference between failure() and always()?

failure() runs when a failure has occurred.
always() runs regardless of whether the workflow succeeded or failed.
failure() → Failure only
always()  → Success + Failure

Q8. Why is failure handling important in CI/CD?

A production pipeline should not simply stop when something fails.
Failure handling can help the DevOps team:

Identify failures
Notify the correct people
Collect diagnostic information
Clean up resources
Start recovery processes
