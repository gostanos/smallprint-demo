# Small Print (MCP) lock demo

[![Small Print check](https://github.com/gostanos/smallprint-demo/actions/workflows/small-print.yml/badge.svg)](https://github.com/gostanos/smallprint-demo/actions/workflows/small-print.yml)

This repository shows what the Small Print check does in a build. It has one MCP server in `.mcp.json`, the reference filesystem server pinned to 2026.7.4, and one instruction file, `CLAUDE.md`. The file `smallprint.lock` records both, and the workflow runs the check on every push and pull request.

The main branch passes. The open pull request moves the filesystem server to 2026.7.10, and its check fails. That release changed the description of one tool, `read_media_file`, with nothing in the version number to say so; the change is on [the server's entry page](https://smallprint.dev/a/npm/%40modelcontextprotocol/server-filesystem).

To do the same in your repository, from the directory that holds your agents' configuration:

```bash
npx smallprint@0.1.5 lock --project
git add smallprint.lock
```

Then add this step to a workflow:

```yaml
- uses: gostanos/smallprint-action@v1.6
```

The check reads the repository's configuration and instruction files, compares them with the lock, and sends nothing anywhere. When a change is yours, run `lock --project` again and commit the lock.
