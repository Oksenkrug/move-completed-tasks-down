# Move Completed Tasks Down

An [Obsidian](https://obsidian.md) plugin that automatically moves completed tasks to the bottom of their list — 5 seconds after you check them off.

---

## What it does

When you tick a task checkbox, the plugin waits 5 seconds and then silently relocates that task — along with any sub-items nested beneath it — to the end of its sibling group. Incomplete tasks stay exactly where they are. The result is a continuously self-organizing list where finished work sinks to the bottom without any manual drag-and-drop.

If you change your mind and uncheck the task before the 5-second delay expires, the pending move is cancelled and nothing happens.

---

## Features

- **Automatic, delayed sorting** — tasks move 5 seconds after completion, giving you time to undo an accidental check
- **Child-aware** — sub-items nested under a completed task travel with it as a unit
- **Scope-aware** — sorting is limited to the *sibling level* of the checked task; items in a parent or different nested group are never disturbed
- **Stable ordering** — incomplete tasks keep their original relative order; multiple completed tasks accumulate in the order they were completed
- **Cancellable** — unchecking a task before the timer fires cancels the move entirely
- **Code-block safe** — tasks inside fenced code blocks (` ``` `) are never moved
- **All view modes** — works in Source mode, Live Preview, and Reading view
- **Mobile compatible** — works on Obsidian for iOS and Android

---

## Supported task formats

The plugin recognises all standard Markdown task list syntax:

```markdown
- [ ] Bullet dash
* [ ] Bullet asterisk
+ [ ] Bullet plus
1. [ ] Numbered list
```

Completion is detected for both lowercase and uppercase `x`:

```markdown
- [x] completed (lowercase)
- [X] completed (uppercase)
```

---

## How it works — step by step

1. You open a note and check off a task.
2. The plugin detects the change (by diffing the file before and after the save).
3. A 5-second timer is started for that specific task.
4. When the timer fires, the plugin re-reads the file (in case you made other edits), locates the task, and moves it — together with any indented children — to the bottom of its sibling scope.
5. The file is saved silently in the background; your cursor position and undo history are unaffected.

### Nested list example

Given this list:

```markdown
- [ ] Buy groceries
    - [x] Eggs
    - [ ] Milk
    - [ ] Bread
- [ ] Call the bank
```

Five seconds after checking **Eggs**, the list becomes:

```markdown
- [ ] Buy groceries
    - [ ] Milk
    - [ ] Bread
    - [x] Eggs
- [ ] Call the bank
```

Only the siblings inside **Buy groceries** are reordered. The top-level items are untouched.

---

## Installation

### From the Obsidian community plugins browser (recommended)

1. Open **Settings → Community plugins**.
2. Make sure **Restricted mode** is off.
3. Click **Browse** and search for **Move Completed Tasks Down**.
4. Click **Install**, then **Enable**.

### Manual installation

1. Download `main.js` and `manifest.json` from the [latest release](../../releases/latest).
2. Create a folder at `<your vault>/.obsidian/plugins/move-completed-tasks-down/`.
3. Copy both files into that folder.
4. In Obsidian, go to **Settings → Community plugins** and enable **Move Completed Tasks Down**.

---

## Settings

This plugin has no configuration options. It works automatically once enabled.

---

## Compatibility

| Requirement | Version |
|---|---|
| Obsidian | 1.0.0 or later |
| Desktop | Yes |
| Mobile | Yes |

---

## FAQ

**Will it move tasks I have already completed before installing the plugin?**
No. The plugin only reacts to tasks that are checked off while it is running. Pre-existing completed tasks are left in place.

**What if I edit the file right after checking a task?**
The plugin re-reads the file when the 5-second timer fires, so it always operates on the latest content. It searches a small window around the original line number to locate the task even if lines shifted due to your edits.

**Does it work with Dataview or Tasks plugin checkbox states like `- [/]` or `- [-]`?**
No. Only `[x]` and `[X]` are treated as completed. All other custom states are ignored.

**Can the 5-second delay be changed?**
Not currently. A settings panel to configure the delay is planned for a future release.

**Is my vault modified unexpectedly?**
The plugin only writes to a file when at least one completed task is out of order in its sibling scope. If the list is already sorted, it does nothing.

---

## Contributing

Pull requests and issues are welcome. To build from source:

```bash
git clone https://github.com/<your-username>/obsidian-move-completed-tasks-down
cd obsidian-move-completed-tasks-down
npm install

# Development build (watches for changes)
npm run dev

# Production build
npm run build
```

Copy `main.js` and `manifest.json` into your vault's plugin folder to test.

---

## License

[MIT](LICENSE)
