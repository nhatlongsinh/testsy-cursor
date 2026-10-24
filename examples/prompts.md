# Try a Testsy workflow

Replace the example address with a staging site you are authorized to test. Select an existing Testsy project and configure its sign-in accounts in the app when needed.

**Release check**

> Use testsy-check-release to check https://staging.example.com. In project p_myproject, reuse the saved login and create-note tests. Run each once and show the evidence and any coverage gaps. Do not create schedules or public links.

**Failed-run investigation**

> Use testsy-investigate-run to inspect j_myrun. Tell me what the test expected, what was observed, and whether the evidence supports an app bug. Prepare a fix handoff. Do not rerun it yet.

**Regression from a bug**

> Use testsy-regression-from-bug for this fixed bug: editing a note showed a saved message but reverted its title after reload. On https://staging.example.com, sign in using the existing "QA member" account, create a synthetic note, change its title, reload, and independently check the new title persists. Show me the plan before saving and running one test.

In Codex, invoke skills as `$testsy-check-release`, `$testsy-investigate-run` and `$testsy-regression-from-bug`. Plugin hosts may prefix skill names with the plugin namespace. Use the names exposed by your client's skill list.
