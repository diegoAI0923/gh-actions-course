# GitHub Actions Lecture Notes

Structured notes from course transcripts shared for GitHub Actions certification preparation.

## Workflow events

**Concept:** Workflow events are triggers that start a GitHub Actions workflow.

**Key idea:** A workflow can listen for one or more events. GitHub Actions runs the workflow when a matching event occurs.

### Repository events

Repository activity can trigger workflows. Common examples include:

- `push` when commits or tags are pushed.
- `issues` when an issue is created, edited, closed, or otherwise updated.
- `pull_request` when a pull request is opened, closed, or synchronized.
- `pull_request_review`, `fork`, `release`, deployment, and project-related events.

Events can be filtered by configuration such as branches or activity types.

```yaml
on:
  push:
    branches: [main]
  pull_request:
    types: [opened, synchronize]
```

> This workflow runs for pushes to `main` and when a pull request is opened or synchronized. The values in `types` are activity types: specific variations of an event.

### Manual and programmatic triggers

```yaml
on:
  workflow_dispatch:
```

> `workflow_dispatch` enables a manual run from the **Run workflow** button in the repository's **Actions** tab. It can also be triggered through GitHub's supported workflow-dispatch API.

Reusable workflows can be called from another workflow with `workflow_call`.

```yaml
on:
  workflow_call:
```

> A reusable workflow uses `workflow_call` to declare that another workflow may invoke it.

### Scheduled triggers

```yaml
on:
  schedule:
    - cron: "0 9 * * 1-5"
```

> `schedule` runs a workflow automatically according to a POSIX cron expression. This example runs at 09:00 UTC every weekday.

### Multiple triggers

```yaml
on: [push, pull_request]
```

> List syntax enables more than one trigger for the same workflow. The workflow runs when either event occurs.

### Documentation

GitHub provides a comprehensive list of supported events and their activity types. Consult it instead of attempting to memorize every event:

- [Events that trigger workflows](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows)

**Key takeaway:** Select workflow events based on the repository activity that should start automation. Use filters and activity types to narrow when a workflow runs, and use manual, reusable, or scheduled triggers when repository activity is not the right trigger.
