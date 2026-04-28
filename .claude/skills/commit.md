# Commit Skill

A skill for creating well-formed, linted commits following Conventional Commits and project best practices.

## Trigger

When the user runs `/commit`.

## Instructions

Follow these steps exactly, in order.

### 1. Gather state

Run in parallel:
- `git status` — see what is staged vs unstaged
- `git diff --staged` — review exactly what will be committed
- `git log --oneline -5` — check recent commit style in this repo

### 2. Validate staged changes

If nothing is staged, tell the user and stop. Do not auto-stage everything — ask which files to stage.

### 3. Review the diff for issues

Before writing the commit message, scan the staged diff for:
- Leftover debug code (`console.log`, `Debug.WriteLine`, `TODO` comments added in this diff, hardcoded secrets or credentials)
- Unintended file changes (lock files, `.DS_Store`, `bin/`, `obj/`)

If any are found, list them and ask the user whether to proceed or fix first.

### 4. Write the commit message

Follow **Conventional Commits** (`https://www.conventionalcommits.org`):

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

**Types:**
- `feat` — new feature
- `fix` — bug fix
- `refactor` — code change that is not a fix or feature
- `test` — adding or updating tests
- `chore` — build, tooling, dependencies
- `docs` — documentation only
- `style` — formatting, no logic change
- `perf` — performance improvement
- `ci` — CI/CD changes

**Rules:**
- Subject line: imperative mood, lowercase after the colon, no trailing period, max 72 chars
- Scope: the layer or module affected (e.g. `domain`, `application`, `infrastructure`, `api`, `tests`)
- Body: explain *why*, not *what* — the diff already shows what changed
- If the change closes a GitHub issue, add `Closes #<number>` in the footer

**Examples:**
```
feat(application): add CreateTodo command and handler
fix(infrastructure): handle missing userId in DynamoDB query
test(application): add unit tests for CreateTodoHandler
chore: add .gitignore for bin and obj directories
```

### 5. Lint the commit message

Before committing, verify:
- [ ] Type is one of the allowed types above
- [ ] Subject is ≤ 72 characters
- [ ] Subject uses imperative mood (starts with a verb: add, fix, remove, update, rename…)
- [ ] Subject does not end with a period
- [ ] No `WIP` or placeholder text
- [ ] No sensitive data in message

If any check fails, rewrite the message before proceeding.

### 6. Show the commit message to the user

Display the final message and ask for confirmation before running `git commit`.

### 7. Commit

```bash
git commit -m "$(cat <<'EOF'
<message here>
EOF
)"
```

After committing, run `git log --oneline -1` and show the result to confirm.

### 8. Ask about pushing

Ask the user: "Push to remote now?" — do not push without explicit confirmation.
