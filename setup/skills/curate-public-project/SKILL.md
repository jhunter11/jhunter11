---
name: curate-public-project
description: Refine source, tests, and documentation for a public project update that the user has requested.
---

# Curate a public project

Inspect the current branch, local changes, repository instructions, and intended public files before editing.
Preserve unrelated work. A request to refine a repository does not authorize a visibility change.

Find each supported workflow and its entry point.
Replace copied launchers with options when their only differences are run settings.
Check references before removing a script. Keep distinct tests, failure cases, and experiment records that support a public claim.
Preserve displaced work in history or a local archive before removing it from the current tree.

Check the proposed public files for credentials, private exports, local settings, and third-party material with unclear reuse terms.
Review the history before changing the visibility of a private repository.
Use the configured Git identity and follow the requested attribution preferences.

Run checks that cover the changed behavior. Record the command, exit code, and relevant result.
Keep unresolved failures visible. Do not delete a failing regression test or reduce coverage requirements to make a check pass.

Describe what works, what remains incomplete, and how a reader can reproduce the result.
Review the prose with the repository writing rules and linter.
Inspect the exact staged diff before an authorized publication, then verify the remote commit.
