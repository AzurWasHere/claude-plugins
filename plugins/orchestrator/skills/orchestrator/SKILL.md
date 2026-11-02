---
name: orchestrator
description: Work GitHub issues end to end with the Opus orchestrator. Grills issues that lack acceptance criteria, runs the rest in parallel background agents.
disable-model-invocation: true
argument-hint: "[issue numbers...]"
---
You are the lead for this run, in the user's own session. Issues: $ARGUMENTS

1. **Gates exist.** Read `AGENTS.md` at the repo root. Without it, or without a `## Gates` section, tell the user to run `/orchestrator:init` and stop.

2. **Sort the issues.** For each number, run `gh issue view <n> --json number,title,body,state`. An open issue whose body has an `## Acceptance criteria` heading with `- [ ]` items is **grilled**; every other issue, and no issue numbers at all, is **ungrilled** work.

3. **Start every grilled issue now**, in one message: one Agent call per issue with `subagent_type: "orchestrator:orchestrator"`, `run_in_background: true`, and the prompt `Issue worker for #<n> in <owner/repo>. Run the pipeline for this issue only.` There is no concurrency cap.

4. **Grill the ungrilled work**, one item at a time, while the started issues run. Use the `mattpocock-skills:grilling` skill; if it is not installed, tell the user to run `claude plugin install mattpocock-skills@ai-bible` and stop grilling. When the user confirms shared understanding, write the issue body yourself, ending with `## Acceptance criteria` and a `- [ ]` checklist of checkable outcomes. Spawn `orchestrator:chore` to create the issue (or replace the existing issue's body) with that text verbatim, then start it as in step 3.

5. **Relay.** A background agent that ends with `QUESTION #<n>: ...` is waiting on the user: ask the user that question, then send the answer with `SendMessage` to that same agent. `NOT GRILLED #<n>` sends the issue to step 4. `NO GATES` repeats step 1's message.

6. **Report.** For each `DONE #<n>: <PR url>`, tell the user in one line. The run is finished when every issue has a PR or is waiting on the user.
