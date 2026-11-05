# Issue tracker: GitHub

Issues and specs live in GitHub Issues for `hvkooten/my-contoso-workshop`. Use the `gh` CLI for issue operations.

## Conventions

Before the first issue creation in a session, verify the target with `gh repo view --json nameWithOwner`. Use `--repo hvkooten/my-contoso-workshop` explicitly if the inferred target differs. File this project's issues in this repository.

- **Create**: `gh issue create --repo hvkooten/my-contoso-workshop --title "..." --body "..."`. For multi-line bodies, use `--body-file <path>` or pipe a PowerShell here-string to `--body-file -`.
- **Read**: `gh issue view <number> --json number,title,body,labels,comments`.
- **List**: `gh issue list --state open --json number,title,body,labels,comments`, with appropriate `--label` and `--state` filters.
- **Comment**: `gh issue comment <number> --body "..."`.
- **Apply / remove labels**: `gh issue edit <number> --add-label "..."` / `--remove-label "..."`.
- **Close**: post the explanation with `gh issue comment <number> --body "..."`, then `gh issue close <number>`. Posting the comment separately also preserves explanations for already-closed issues.

### Sub-issues and blockers

Use GitHub's native sub-issues and issue dependencies when available:

- **Sub-issue** (`gh` 2.94+): `gh issue create --parent <parent> ...`, or `gh issue edit <parent> --add-sub-issue <child>`.
- **Blockers** (`gh` 2.94+): `gh issue create --blocked-by <n>,<n> ...`, or `gh issue edit <child> --add-blocked-by <blocker>`.
- **Older CLI, sub-issue**: `gh api --method POST repos/hvkooten/my-contoso-workshop/issues/<parent>/sub_issues -F sub_issue_id=<child-db-id>`.
- **Older CLI, blocker**: `gh api --method POST repos/hvkooten/my-contoso-workshop/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`.

Obtain database IDs with `gh api repos/hvkooten/my-contoso-workshop/issues/<number> --jq .id`; API writes above require that numeric ID, not an issue number or node ID.

If sub-issues are unavailable, put `Part of #<parent>` at the top of the child body and add the child to a task list in the parent. If dependencies are unavailable, put `Blocked by: #<n>, #<n>` at the top of the child body. A ticket is unblocked when every blocker is closed.

Count open native blockers with `gh api repos/hvkooten/my-contoso-workshop/issues/<number> --jq .issue_dependencies_summary.blocked_by`. If using `gh issue view <number> --json blockedBy`, filter to blockers whose state is `OPEN`.

## Pull requests as a triage surface

**PRs as a request surface: no.**

Set this flag to `yes` if external PRs should enter the triage queue. When enabled:

- Read both the body and comments with `gh pr view <number>` and `gh pr view <number> --comments`; inspect changes with `gh pr diff <number>`.
- List external requests with `gh api --paginate 'repos/hvkooten/my-contoso-workshop/pulls?state=open' --jq '.[] | select(.author_association | IN("OWNER","MEMBER","COLLABORATOR") | not) | {number, title, author: .user.login, author_association, labels: [.labels[].name]}'`.
- Use `gh pr comment`, `gh pr edit --add-label` / `--remove-label`, and `gh pr close` for triage operations.

GitHub shares issue and PR numbers. Resolve ambiguous numbers with `gh pr view <number>` and fall back to `gh issue view <number>` only when the item is not a PR.

## Skill operations

When a skill says **publish to the issue tracker**, create a GitHub issue. When it says **fetch the relevant ticket**, read the issue and its comments.

### Wayfinding

The map is a single issue with child issues as tickets:

- **Map**: label `wayfinder:map`, with Notes / Decisions-so-far / Fog in the body.
- **Child**: link as a sub-issue, using the fallback above when needed. Label `wayfinder:<type>`, where type is `research`, `prototype`, `grilling`, or `task`.
- **Frontier**: list the map's open children, exclude assigned tickets and tickets with open blockers, and take the first remaining ticket in map order.
- **Claim**: `gh issue edit <number> --add-assignee @me`, the session's first write.
- **Resolve**: comment with the answer, close the ticket, and append a gist and link to the map's Decisions-so-far.

Ensure required wayfinder labels exist before applying them.
