---
name: testsy-regression-from-bug
description: Turn a reported or fixed web-app bug into a saved Testsy regression test with independent expectations, then verify the fix when running is authorized.
---

# Turn a bug into a Testsy regression test

Use the connected Testsy MCP tools. Extract the target URL/project, reproduction trigger, original expected behavior, necessary setup and any existing failing run from the request. Read `get_run` and `get_test` when ids are supplied. Do not derive the expected behavior from the implementation or from whatever the broken app currently shows.

Check `list_tests` for matching coverage and inspect candidates with `get_test`. Reuse a suitable saved test. If an existing check needs correction, preserve its original requirement and failed attempt, explain the business-rule reason for the change and use the requester's authorization; do not silently broaden or weaken it.

Draft a small test with `plan_test` using `description`, `url` and `projectId`. Express the bug's trigger as actions and the expected behavior as independently verifiable checks. Record values that make the comparison reproducible. Specify persistence after reload or a second session only when it belongs to the bug. Use synthetic records, and name existing sign-in accounts instead of embedding credentials.

Show the proposed plan, assumptions and questions. Resolve questions with `answers`, or revise using `plan` and `change`. After confirmation (including existing explicit approval of the exact plan), call `create_test` with the plan or update the authorized saved test. Do not activate a schedule as part of saving coverage.

When the requester authorizes execution, use `run_test` and `wait_run` (repeat while `final` is false) until `final`, within their deadline/run allowance. If a safe pre-fix build is available and the requester wants reproduction, the same check should demonstrate the original mismatch there. Do not reintroduce the defect into a live environment to create that proof. If only the fixed build is available, label the result as post-fix verification; it does not prove pre-fix reproduction.

Return the saved test id, unchanged acceptance criteria, run ids/links and the expected versus observed result. Preserve failures and distinguish app mismatch from blocked/inconclusive/error execution. Suggest CI or a schedule only as a next step; configure it only when requested.
