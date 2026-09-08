# Reuse my agent setup

These are the parts of my setup that I can share: a local memory MCP server, project context templates, and three skills.
The installers live with their source and tests. Each skill is a short Markdown file that you can inspect before use.

## Local memory through MCP

[Multi-Agent Memory MCP](https://github.com/jhunter11/multi-agent-memory-MCP) stores records in SQLite and retrieves them through text search and a typed graph.
It works with a local MCP client. The server has no model dependency or hosted account.
Use a separate database for each trust boundary. Its scope labels do not enforce access control.

The [setup guide](https://github.com/jhunter11/multi-agent-memory-MCP#install) covers Windows, macOS, and Linux.
The default script installs dependencies and runs checks. It leaves client settings unchanged.
You can then print a client configuration and review the paths before writing it.

The [client examples](https://github.com/jhunter11/multi-agent-memory-MCP/tree/main/examples/clients) cover Claude Code, Codex, and OpenCode.
The repository also has examples for local models through Ollama, LM Studio, and vLLM.
The MCP client and selected model must support tool calls.

## Shared project context

[Team memory kit](https://github.com/jhunter11/avp-team-memory) shares project facts and decisions across coding tools through local files.
Its Python installer previews changes by default. The `--apply` option writes the reviewed changes into an existing project.
The kit starts with blank memory files and preserves existing records.

The kit includes a context builder and adapters for Codex, Claude Code, Gemini CLI, Copilot, and Cursor.
Review the generated context before sharing it with a model provider.

## Curated skills

These skills capture review habits from my projects. They are instructions for an agent, with no bundled executable code.

| Skill | When to use it |
| --- | --- |
| [Check research claims](skills/check-research-claims/SKILL.md) | Compare a result with its experiment records and separate proposals from measured work |
| [Curate a public project](skills/curate-public-project/SKILL.md) | Prepare a requested public release with one supported path per workflow and relevant tests |
| [Review project context](skills/review-project-context/SKILL.md) | Update shared facts, decisions, and open questions from source evidence |

Download this repository and copy the selected skill folder into the skill directory supported by your agent.
Keep the folder name and `SKILL.md` together. These files also work as instructions that you read and apply manually.
They do not install an MCP server or change an agent's permissions.

For prose edits, I also use Peter Yang's [no-ai-slop](https://github.com/petergyang/no-ai-slop) skill.
That link points to the upstream project, which has its own terms and updates.
My writing checks also draw on [Simplified Technical English](https://asd-ste100.org/).
An AI detector score can help flag text for review, but it cannot establish who wrote it.

## What I have checked

On September 8, 2026, the memory MCP release checks passed with 87 tests.
The team memory kit passed five tests.
Those checks cover the versions below. A later change needs its own check.

| Component | Reviewed commit |
| --- | --- |
| Memory MCP | [`c332e74`](https://github.com/jhunter11/multi-agent-memory-MCP/commit/c332e741c8f18267776a94a3fb6fd1621903d30b) |
| Team memory kit | [`54c608f`](https://github.com/jhunter11/avp-team-memory/commit/54c608f9cc92eb0f892787788917c81f4d142e38) |

I checked the skill files for structure, writing, and scope. I have not measured whether they improve agent performance.
Jarvis Control remains a separate development project with unresolved tests. It is outside this starter setup.

The original files in this `setup` directory use the [MIT license](LICENSE).
Linked projects retain their own licenses.
