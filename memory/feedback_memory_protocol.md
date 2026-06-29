# Memory Protocol

When the user corrects Codex or asks Codex to remember something about this workspace, save it as its own Markdown file in `memory/`.

Use these filename prefixes:

- `user_` for how the user personally works.
- `project_` for this specific project.
- `feedback_` for corrections to Codex behaviour.
- `reference_` for links, facts, or external context to remember.

Keep `memory/MEMORY.md` updated as an index of every memory rule with a one-line summary, so the right context loads next session.

Maintain two companion files:

- `memory/lessons.md`: narrative strategic learnings. When the user says something is a "lesson" or "pattern we should remember," or when the same kind of correction repeats, append an entry with what happened, why it was wrong, what changed, and the deeper principle.
- `tasks/todo.md`: active sprint work. Plan here before building and mark items complete as they ship.

At the start of every new session, read `memory/MEMORY.md`, `memory/lessons.md`, and `tasks/todo.md` before continuing.
