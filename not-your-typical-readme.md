# GitHub Actions Certification Study Notes

## Publishing a local repository to GitHub

**Goal:** Initialize this local folder as a Git repository and publish it to GitHub.

```sh
git init
```

> Creates a new local Git repository in the current folder by adding Git's hidden metadata directory.

```sh
git remote add origin https://github.com/diegoAI0923/gh-actions-course.git
```

> Registers this GitHub repository as the remote named `origin`, giving local Git commands a destination for fetching and pushing.

```sh
git branch -M main
```

> Renames the current branch to `main`, replacing an existing branch named `main` if necessary.

```sh
git add .
```

> Stages all non-ignored changes in the current repository so they are included in the next commit.

```sh
git commit -m "<message>"
```

> Creates a local commit from the staged changes and labels it with the message in place of `<message>`.

```sh
git push -u origin main
```

> Uploads the local `main` branch to `origin` and records it as the branch's upstream, so later `git push` and `git pull` commands can omit the remote and branch names.

**Reference:** [Udemy course lecture](https://www.udemy.com/course/mastering-github-actions-beginner-to-expert/learn/lecture/41691464#overview)

## Reusable study entry

Use this structure whenever recording work in this repository.

### [Topic or workflow name]

**Concept:** What GitHub Actions or Git capability is being practiced?

**Context:** What problem, goal, or repository state led to this work?

**Commands or configuration:**

```sh
# Replace with the command or configuration being studied.
```

> Explain what the command or configuration does and why it matters here.

**Observed result:** Record the output, workflow behavior, or repository change that confirmed the result.

**Key takeaway:** Capture the certification-relevant idea in one or two sentences.

**References:** Link the course lecture, GitHub documentation, or other source used.


## YAML in 5 minutes

**Concept:** YAML is a human-readable data format used to define GitHub Actions workflows.

**Context:** These are the YAML building blocks needed when reading and writing workflow configuration.

```yaml
key: value
```

> A mapping stores a value under a key. YAML uses indentation, rather than braces, to show nested structure.

```yaml
name: GitHub Actions
retries: 3
enabled: true
```

> YAML supports scalar values such as strings, numbers, and booleans. A YAML parser determines their types, but YAML alone does not enforce a schema.

```yaml
config:
  path: first-directory/file.yaml
  environment: staging
```

> A nested mapping groups related key-value pairs. Its child keys must be indented (child-parent relationship) consistently beneath `config`.

```yaml
colors:
  - red
  - green
  - blue
  - 10
```

> A hyphen starts each item in a sequence (also called an array or list). Sequence items can contain values of different types unless a separate schema restricts them.

```yaml
colors:
  - name: red
    hex: ff0000
```

> A sequence item can itself be a mapping, allowing YAML values to represent more complex objects.

**Key takeaway:** GitHub Actions workflow files use YAML mappings, sequences, and indentation to represent nested configuration.


## GitHub Actions building blocks

**Concept:** A workflow contains jobs, and each job contains the steps that perform the work.

**Context:** Understanding this hierarchy makes it easier to read and build GitHub Actions workflow files.

### Workflows

> A workflow is a YAML file configured at the repository level. It contains at least one job and starts when one of its configured triggers occurs.

### Triggers

```yaml
on:
  push:
  workflow_dispatch:
```

> The `on` key lists the events that start a workflow. `push` runs the workflow when commits or tags are pushed, and `workflow_dispatch` enables a manual run from the **Run workflow** button in the repository's **Actions** tab.

> `workflow_dispatch:` has no inputs in this example. The workflow file must be on the default branch before GitHub shows its manual-run button.

### Empty trigger configuration

> YAML permits a key with no value; its value is `null`. GitHub Actions treats an empty event configuration as a request to enable that event with its default behavior.

```yaml
on: [push, workflow_dispatch]
```

> This list syntax is equivalent to the previous mapping when neither event needs additional configuration.

```yaml
on:
  push:
    branches: [main]
```

> Add nested values only when the event needs configuration. This example restricts the `push` trigger to the `main` branch.

### Jobs

> Jobs are defined under the workflow's `jobs` key. Each job specifies its execution environment with `runs-on` and runs in parallel with other jobs by default unless dependencies are declared with `needs`.

### Steps

> Steps belong to a job and define the commands or actions it performs. The steps in a job run sequentially by default.

**Hierarchy:** Workflow -> Jobs -> Steps

```yaml
name: workflow-a

on: push

jobs:
  A:
    runs-on: ubuntu-latest
    steps:
      - run: echo "hello world"
  B:
    runs-on: ubuntu-latest
    steps:
      - run: echo "bye world"
```

> This workflow runs when code is pushed to the repository. It has two independent jobs, `A` and `B`, which run on Ubuntu runners and each execute one shell command.

### Step syntax

```yaml
steps:
  - name: Say Hello
    run: echo "hello, world!"
```

> A step is one list item. Its `name` and `run` properties must be indented beneath the same hyphen. A step must provide `run` or `uses`; `name` alone is not executable.

**Key takeaway:** Workflows coordinate jobs, jobs select a runner and organize steps, and steps perform the individual actions or commands.
