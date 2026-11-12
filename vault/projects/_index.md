---
type: index
updated: [SYNC_START_DATE]
source: kept by the agents, from what [YOUR_FIRST_NAME] says
workstream_field: {the id of the "Workstream" field in [TASK_MANAGER], or: not created yet}
---

# [YOUR_ORG] workstreams: the registry

Why it matters: this is the one list agents use to connect a task to a workstream and a workstream to a goal. The workstream field in [TASK_MANAGER] (if you make one) uses exactly these names. The slug is the folder name under `projects/`.

| Slug | Workstream | Kind | Goal | Memo code | Owner | Task homes | Overview |
|---|---|---|---|---|---|---|---|
| example-workstream | Example workstream | area | {goal in me/goals.md} | PROG | [YOUR_FIRST_NAME] | {project or section in [TASK_MANAGER]} | [[projects/example-workstream/overview]] |

Kinds: `area` runs for as long as the organisation does (a program, an operations function); `project` has an end (an event, a deliverable, a cohort); `archived` is kept for history only. A cohort or a one-time event is a project inside its area.

How to use it:
1. A task's workstream is, in this order: its workstream field value; the value of its parent task (a subtask takes its parent's); the project or parent task listed under "Task homes".
2. A task with no field value and no traceable home is unlabelled. A match on words in its name is a proposal, not a value: list it for [YOUR_FIRST_NAME] to confirm.
3. Resolve people before classifying: `people/_team.md`, `people/_index.md`, and `people/_settled.md` for names settled before.
4. The Goal column points into `me/goals.md`; each workstream has exactly one goal.
5. The Memo code is one of the workstream codes of Memo (`local/workstreams.json` in the Memo app).

## Change log
One line per change: `YYYY-MM-DD, what changed, why, source`
