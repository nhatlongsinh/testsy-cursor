---
name: testsy-check-release
description: Check a website release with Testsy, using saved tests or a plain-English test plan and reporting the browser evidence. Use when the requester wants Testsy release or smoke checks.
---

# Check a release with Testsy

Use the connected Testsy MCP tools. If unavailable, explain that a workspace connection is required and point to the Testsy MCP documentation. Do not pretend to have run a test.

Identify the target URL, project and release-critical behavior from the request. Use `list_projects` and `list_tests` to locate existing tests; read `get_test` before assuming what a saved test checks. Prefer those tests over creating duplicates.

For a new test, call `plan_test` with `description`, `url` and `projectId`. It uses the workspace's daily assistant allowance. Show the proposed actions, independent expected checks and questions. Resolve unanswered business rules; do not invent expected values. Use `plan` plus `change` to revise, or `answers` keyed by question id. Save with `create_test` after the requester confirms the plan; existing explicit approval of that exact plan suffices. Name existing sign-in credentials rather than putting passwords in the requirement. An email signup check needs the test's email service enabled in its options; follow the discovered tool schema.

Use the requester's authorization for the selected runs and effects. A test can create records, send mail or perform purchases on the target: keep those within the agreed test environment and scope. Do not enable schedules, share links or run unrelated suites as a side effect of a release check.

Start with `run_test`, or `run_project` for an explicitly requested suite. Record every returned run id and every skipped test, and give the requester each run's `watchUrl` right away: it opens the run live, and its result afterwards, without a Testsy sign-in (absent when the workspace turned watch links off). Wait with `wait_run` (one call waits up to 55 seconds and returns the run the moment it is final; call it again while `final` is false) instead of polling `get_run` every few seconds. Reuse the existing run id after a lost response when available; do not repeatedly start paid runs to obtain status. Respect the requester's time/run limit and stop polling with the unfinished run link if it expires. Further runs after a terminal error need a supported reason and remaining authorized allowance.

Report the original expectation, observed value, check outcome and available result/evidence links. A legitimate mismatch is an application failure; `blocked`, `inconclusive`, `error`, `cancelled` and skipped tests do not establish a pass. State coverage gaps and distinguish suspected engine limitations from proven app defects. Do not weaken a failing check to make the release pass. After a fix, rerun the same test when authorized and link both attempts.
