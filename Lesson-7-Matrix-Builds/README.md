# GitHub Actions Lesson 7 — Matrix Builds

## 1. Objective

The objective of this lesson was to understand and implement **Matrix Builds** in GitHub Actions.
A matrix strategy allows the same job to run with multiple combinations of configurations such as:

* Operating systems
* Programming language versions
* Application versions
* Environments
* Other configuration values

In this hands-on exercise, I tested the application using:

* Ubuntu
* Windows
* Node.js 20
* Node.js 22

This created four automatic test combinations.

# 2. What is a Matrix Build?

A Matrix Build allows GitHub Actions to run the same job multiple times with different 
configuration values.
Instead of creating separate jobs manually, we define the configuration once using:

```yaml
strategy:
  matrix:
```
GitHub Actions automatically creates the required combinations.

Example:

```yaml
strategy:
  matrix:
    os:
      - ubuntu-latest
      - windows-latest

    node-version:
      - 20
      - 22
```

This creates:

```text
Ubuntu + Node 20
Ubuntu + Node 22
Windows + Node 20
Windows + Node 22
```

Therefore:

```text
2 Operating Systems × 2 Node Versions = 4 Jobs
```

# 3. What is `strategy.matrix`?

`strategy.matrix` defines the different configurations that GitHub Actions should test.

Example:

```yaml
strategy:
  matrix:
    os:
      - ubuntu-latest
      - windows-latest
    node-version:
      - 20
      - 22
```

The `strategy` defines how the job should be executed.
The `matrix` defines the different values that should be used.

# 4. Matrix Configuration Used in This Lesson

The workflow used:

```yaml
strategy:
  matrix:
    os:
      - ubuntu-latest
      - windows-latest

    node-version:
      - 20
      - 22
```

The resulting combinations were:

| Operating System | Node.js Version | Result   |
| ---------------- | --------------: | -------- |
| Ubuntu           |              20 | ✅ Passed |
| Ubuntu           |              22 | ✅ Passed |
| Windows          |              20 | ✅ Passed |
| Windows          |              22 | ✅ Passed |

All four combinations completed successfully.

# 5. `matrix.os`

The following expression was used:

```yaml
runs-on: ${{ matrix.os }}
```

`matrix.os` contains the operating system currently being tested.

For example:

```text
matrix.os = ubuntu-latest
```

or:

```text
matrix.os = windows-latest
```

GitHub Actions automatically creates a separate job for each operating system.

# 6. `matrix.node-version`

The workflow used:

```yaml
node-version: ${{ matrix.node-version }}
```

This tells the `actions/setup-node` action which Node.js version should be installed.
The matrix contained:

```text
Node 20
Node 22
```

Therefore, each operating system was tested against both Node.js versions.

# 7. Matrix Build Combinations

The matrix created four combinations:

```text
                 MATRIX
                    |
          +---------+---------+
          |                   |
       Ubuntu               Windows
          |                   |
      +---+---+           +---+---+
      |       |           |       |
   Node 20 Node 22     Node 20 Node 22
      |       |           |       |
      v       v           v       v
     PASS    PASS        PASS    PASS
```

The important point is that these combinations are generated automatically from one job 
definition.

# 8. Parallel Execution

Matrix jobs can run independently and can execute in parallel.

Instead of:

```text
Ubuntu + Node 20
       ↓
Ubuntu + Node 22
       ↓
Windows + Node 20
       ↓
Windows + Node 22
```

GitHub Actions can execute them concurrently:

```text
Ubuntu + Node 20 ──┐
Ubuntu + Node 22 ──┤
Windows + Node 20 ─┼──→ Results
Windows + Node 22 ─┘
```

This can reduce the total testing time when multiple configurations need to be tested.

# 9. Workflow Used

The Lesson 7 workflow was stored at:

```text
.github/workflows/lesson7.yml
```

The important matrix section was:

```yaml
strategy:
  matrix:
    os:
      - ubuntu-latest
      - windows-latest

    node-version:
      - 20
      - 22
```

The operating system was selected using:

```yaml
runs-on: ${{ matrix.os }}
```

The Node.js version was selected using:

```yaml
node-version: ${{ matrix.node-version }}
```

The workflow also used:

```yaml
uses: actions/checkout@v4
```

to check out the repository and:

```yaml
uses: actions/setup-node@v4
```

to configure the required Node.js version.

# 10. Why Companies Use Matrix Builds

Matrix builds are useful when an application supports multiple configurations.
For example, a company may need to test:

```text
Operating Systems:
- Ubuntu
- Windows
- macOS

Node.js:
- 20
- 22

```

Instead of creating six separate jobs manually, a matrix can generate all combinations.
Example:

```text
3 Operating Systems × 2 Node Versions = 6 Test Jobs
```

Common use cases include:

* Testing multiple operating systems
* Testing multiple programming language versions
* Testing different database versions
* Testing different browser versions
* Testing multiple application configurations
* Cross-platform compatibility testing

# 11. Matrix Builds vs Normal Jobs

### Without Matrix

We might create:

```text
Job 1 → Ubuntu + Node 20
Job 2 → Ubuntu + Node 22
Job 3 → Windows + Node 20
Job 4 → Windows + Node 22
```

This creates duplicated workflow code.

### With Matrix

We define the configuration once:

```yaml
strategy:
  matrix:
    os:
      - ubuntu-latest
      - windows-latest
    node-version:
      - 20
      - 22
```

GitHub Actions creates the combinations automatically.

Therefore, matrix builds make workflows:

* Cleaner
* Easier to maintain
* Less repetitive
* Easier to expand

---

# 12. Jenkins Equivalent

Jenkins can also run the same tests against multiple configurations.

Modern Jenkins Pipeline can use matrix-style stages.

A simplified example is:

```groovy
pipeline {
    agent none

    stages {
        stage('Test') {
            matrix {
                axes {
                    axis {
                        name 'OS'
                        values 'linux', 'windows'
                    }

                    axis {
                        name 'NODE_VERSION'
                        values '20', '22'
                    }
                }

                stages {
                    stage('Run Tests') {
                        steps {
                            echo "Testing ${OS} with Node ${NODE_VERSION}"
                        }
                    }
                }
            }
        }
    }
}
```

The concept is similar:

```text
GitHub Actions                 Jenkins

strategy.matrix        →       matrix

matrix.os              →       OS axis

matrix.node-version    →       NODE_VERSION axis
```

Both approaches help test multiple configurations without duplicating the complete pipeline.

# 13. Interview Questions

## Q1. What is a Matrix Build in GitHub Actions?

A Matrix Build allows the same job to run against multiple combinations of configuration values.

For example, an application can be tested against multiple operating systems and programming 
language versions.

## Q2. What is `strategy.matrix`?

`strategy.matrix` defines the configuration values that GitHub Actions should use to create 
 multiple job combinations.

## Q3. How many jobs are created by this matrix?

```yaml
matrix:
  os:
    - ubuntu-latest
    - windows-latest

  node-version:
    - 20
    - 22
```

Answer:

```text
2 × 2 = 4 jobs
```

## Q4. What is `${{ matrix.os }}`?

It refers to the current operating system value selected by the matrix.

Example:

```yaml
runs-on: ${{ matrix.os }}
```

## Q5. What is `${{ matrix.node-version }}`?

It refers to the current Node.js version selected by the matrix.

## Q6. Why use Matrix Builds instead of creating multiple jobs manually?

Matrix builds reduce duplicated YAML code and make it easier to test multiple configurations.
If another Node.js version needs to be tested, we can simply add it to the matrix.

## Q7. Do matrix jobs have to run sequentially?

No.
Independent matrix combinations can run in parallel, subject to available runner capacity and 
workflow configuration.

## Q8. Give a real-world example of Matrix Builds.

A company supports:

```text
Ubuntu
Windows
macOS
```

and:

```text
Node 20
Node 22
```

A matrix can test all six combinations automatically.

# 14. What I Learned

In this lesson I learned:

* What Matrix Builds are
* How `strategy.matrix` works
* How GitHub Actions creates matrix combinations
* How to use `matrix.os`
* How to use `matrix.node-version`
* How the same job can run against multiple configurations
* How matrix jobs can run in parallel
* Why companies use matrix testing
* How matrix builds reduce duplicated workflow code
* The Jenkins equivalent of matrix testing

# 15. Result

Successfully completed:
**GitHub Actions Lesson 7 — Matrix Builds**

The workflow successfully created and executed four combinations:

```text
Ubuntu + Node 20       ✅
Ubuntu + Node 22       ✅
Windows + Node 20     ✅
Windows + Node 22     ✅
```

All four matrix combinations passed successfully.
The final workflow demonstrated:

```text
                 Matrix Build
                      |
          +-----------+-----------+
          |                       |
       Ubuntu                  Windows
          |                       |
      +---+---+               +---+---+
      |       |               |       |
   Node 20 Node 22         Node 20 Node 22
      |       |               |       |
      v       v               v       v
      ✅      ✅              ✅      ✅
```

# Key Learning

 A GitHub Actions Matrix Build allows us to run the same job against multiple configurations 
 automatically. It reduces duplicated workflow code and helps ensure that an application works
 across supported operating systems, software versions, and environments.

The practical lesson demonstrated:

```text
2 Operating Systems × 2 Node Versions = 4 Matrix Jobs
```

All four jobs completed successfully.
