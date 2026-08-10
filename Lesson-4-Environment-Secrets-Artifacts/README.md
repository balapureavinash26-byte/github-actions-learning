# GitHub Actions Lesson 4 — Environment Variables, Secrets & Artifacts

## Objective

The objective of this lesson was to understand how GitHub Actions handles:

- Environment variables
- GitHub Secrets
- Build artifacts
- Secure configuration
- Uploading files generated during a workflow

This lesson demonstrates concepts commonly used in real-world CI/CD pipelines.

## 1. Environment Variables

Environment variables allow us to store configuration values that can be reused inside a workflow.

Example:

```yaml
env:
  APP_NAME: GitHub-Actions-Demo
  ENVIRONMENT: Development

These variables were used inside shell commands:

     echo "Application: $APP_NAME"
     echo "Environment: $ENVIRONMENT"

Output
Application: GitHub-Actions-Demo
Environment: Development
--

#1.Why Environment Variables?

They allow configuration to be separated from the actual commands.

For example, the same workflow could use:

Development
Testing
Production

without changing the main workflow logic.

#2. GitHub Secrets

GitHub Secrets are used to store sensitive information securely.

For this training, a dummy secret was created:

DEMO_SECRET

#The secret was accessed in the workflow using:
 
env:
  DEMO_SECRET: ${{ secrets.DEMO_SECRET }}

#The workflow checked whether the secret was available:

  '''Bash'''

if [ -n "$DEMO_SECRET" ]; then
  echo "GitHub Secret is available."
else
  echo "GitHub Secret is NOT available."
  exit 1
fi

#Output
===== SECRET CHECK =====
GitHub Secret is available.

#Important Security Practice

Sensitive information such as:

Passwords
API tokens
Cloud credentials
Docker credentials
Access tokens

should not be hard-coded inside workflow files.

GitHub Secrets should be used instead.
--

#3. Artifacts

An artifact is a file or collection of files generated during a GitHub Actions workflow that can be 
stored and accessed after the workflow completes.

# In this lesson, the workflow created:

build.txt

# The file contained:

Application: GitHub-Actions-Demo
Environment: Development

# The artifact was uploaded using:

- name: Upload Build Artifact
  uses: actions/upload-artifact@v4
  with:
    name: application-build
    path: build.txt

#Artifact Name
application-build

#Artifact File
build.txt
----
