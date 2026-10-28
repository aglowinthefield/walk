# walk

An agent skill that walks a list of action items one at a time, so you don't get a nine-bullet reply you lose track of halfway through.

When a reply would end in several action items, the agent turns them into a **ledger** and asks about one item per turn. Every item ends with one of four outcomes:

- **Do now:** the agent handles it inline, then returns to the ledger.
- **Fork:** the agent hands it off. Small items go to a background subagent. Bigger work goes wherever you escalate work (an issue tracker, a task board, a TODO file). The agent asks you once and remembers the answer.
- **Defer:** the agent writes it to a backlog with enough context to pick it up cold.
- **Drop:** the agent records it as dropped, with a reason.

Each turn shows a progress strip (`✅1 · ✅2 · **3** ← current · 4`) and lettered options with a recommendation, so you can answer with one letter.

## Install

Plain [Agent Skills](https://agentskills.io) format. Works in Claude Code, Codex, Hermes, and any agent that reads `SKILL.md`.

```bash
npx skills add aglowinthefield/walk -g
```

Or clone and symlink:

```bash
git clone git@github.com:aglowinthefield/walk.git ~/code/walk
ln -s ~/code/walk/skills/walk ~/.agents/skills/walk
```

## When it runs

- 4 or more action items: the agent walks them without asking.
- 2 or 3 action items: the agent lists them and asks "Walk these?"
- Saying "just list" skips the walk.
- "What did we forget from the last walk?" searches the backlog and past ledgers.

## State

The skill keeps its state outside any repo, in `~/.agents/walk/`:

- `backlog.md`: open deferred items. A new walk mentions these at the start.
- `ledgers/<date>-<slug>.md`: one file per walk, kept up to date as you go so a long detour doesn't lose your place.
- `preferences.md`: where bigger forks go, and any other standing preferences.

## Status

v0. The design came out of walking its own design questions. Expect changes.
