# @weldable/integration-google-tasks

Google Tasks actions for Weldable.

Part of the [Weldable](https://weldable.ai/) integration library — see [@weldable/integration-core](https://github.com/weldable/integration-core) for the full catalog.

## Install

```bash
npm install @weldable/integration-google-tasks @weldable/integration-core
```

`@weldable/integration-core` is a peer dependency and must be installed alongside this package.

## Usage

```ts
import integration from '@weldable/integration-google-tasks'

// List open tasks
const list = integration.actions.find(a => a.id === 'google_tasks.list_tasks')!

const tasks = await list.execute(
  { tasklist: '@default', showCompleted: false, maxResults: 20 },
  ctx, // ActionContext from your Weldable-compatible host
)

// Create a task with a due date
const create = integration.actions.find(a => a.id === 'google_tasks.create_task')!

await create.execute(
  {
    title: 'Review pull request #42',
    notes: 'Focus on the auth changes',
    due: '2025-02-07T00:00:00.000Z',
  },
  ctx,
)

// Mark a task complete
const update = integration.actions.find(a => a.id === 'google_tasks.update_task')!

await update.execute(
  { task: 'abc123', status: 'completed' },
  ctx,
)
