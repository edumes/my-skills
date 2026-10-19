---
name: test-app
description: Test a project's app end to end by driving its real UI, with Playwright for anything that renders in a browser and Computer Use for native desktop apps, then report what passed and failed with evidence. Use when the user asks to test, QA, or smoke-test an app or feature, or to verify a change in the running app.
argument-hint: "[flows to test | URL]"
---

# Test App

Drive the running app the way a user would, check each flow against what it should do, and report with evidence. Use the easiest tool that can reach the target, run the flows, write the report, then offer to turn the flows that passed into Playwright tests.

Do not change the app's code during a run. A failure goes in the report; fixing it is a separate task the user decides on.

## 1. Decide what to test

- If the user named flows or a URL, test those.
- Otherwise derive flows from the current changes: uncommitted work plus the branch's commits since its merge-base with the main branch. Map each changed file to the screens and actions that reach it. Add a quick smoke of the main screen: it loads, renders, and logs no errors.
- With no changes and no instructions, smoke-test the app's main screens and primary flows.

Done when you have a numbered list of flows, each with its steps and the outcome a user should see. Show the list in a few lines and start; do not wait for approval.

## 2. Pick the tool per flow

Choose the easiest tool that reaches the target:

| Target | Tool |
|---|---|
| Web app, dev server, static site, Storybook | Playwright |
| Electron app | Playwright, attached over CDP: launch the app with `--remote-debugging-port=9222`, then `attach --cdp=http://localhost:9222` |
| Native desktop app (AppKit, SwiftUI, Qt, Tauri on macOS), OS dialogs, system tray, flows across several apps | Computer Use |
| Web flow with one step only the OS can do | Playwright, switching to Computer Use for that step |

Playwright is the default because it reads the DOM and accessibility tree, so it is faster and more precise than reading pixels, and what it does can become a test. Computer Use is for what Playwright cannot reach.

If the right tool is not available, say so, and use the other one only if it can really reach the target. Do not pretend to test.

### Playwright: playwright-cli

Resolve the command once and reuse it: `playwright-cli` if it is on `PATH`; otherwise `npx playwright cli` if the project's Playwright includes it (`npx --no-install playwright cli --help` succeeds); otherwise `npx -y @playwright/cli@latest`. If a browser is missing, run its `install-browser`. `--help [command]` documents every command for the installed version.

Use a named session (`-s=test-app`) so other browsers are left alone. Pass the evidence directory when opening it; every snapshot and screenshot of the session then lands there instead of in the project:

```sh
PLAYWRIGHT_MCP_OUTPUT_DIR=<evidence-dir> playwright-cli -s=test-app open <url>
playwright-cli -s=test-app snapshot                     # element refs (e1, e2, ...)
playwright-cli -s=test-app fill e3 "user@example.com"
playwright-cli -s=test-app click e7
playwright-cli -s=test-app find "Saved"                 # check an expected outcome
playwright-cli -s=test-app console warning              # app errors and warnings
playwright-cli -s=test-app requests                     # failed or unexpected API calls
playwright-cli -s=test-app screenshot --filename=<evidence-dir>/<flow>-<step>.png
playwright-cli -s=test-app close
```

Every action prints the Playwright code it ran. Keep that code for each flow; step 6 reuses it.

Run headless. Pass `--headed` to `open` only when the user wants to watch.

### Computer Use

Use the harness's own desktop-control tools: the Computer Use plugin in Codex, computer use through the Claude desktop app in Claude. If the harness ships a skill for them, read it first and follow its access and safety rules. Take a screenshot before and after each step, and save the ones that show an outcome or a failure to the evidence directory.

## 3. Prepare the run

1. Create an evidence directory outside the project: the session's scratchpad if the harness provides one, otherwise `mktemp -d -t test-app`.
2. Find how the app starts: `package.json` scripts, `Makefile`, `README`, `docker-compose.yml`, `Procfile`. If it is already running (check the port or request the URL), reuse it. Otherwise start it in the background, wait until the URL answers, and record what you started. Ask the user only if you cannot find a start command.
3. If a flow needs login, look for test credentials in the README, `.env.example`, or seed data. Ask if there are none. Never use a real user's account unless the user provides it. After logging in once, `state-save` the session to the evidence directory and `state-load` it in later sessions.

Run destructive or outward-facing actions (deleting data, payments, emails or messages to real people) only against local or test data. Ask before running them anywhere else.

## 4. Run each flow

For each flow, in order:

1. Perform the steps.
2. Check the expected outcome on the page: a snapshot, `find`, or `eval`. A flow passes only when you observed the outcome, not just because nothing errored.
3. Read the console errors and failed requests (4xx, 5xx) since the flow started. Record them even when the flow passed.
4. Screenshot the final state, and the failing state on a failure.

On a failure, retry the flow once from a fresh page to rule out timing. If it fails again, record the step, expected versus actual, and the evidence, then move on to the next flow. If something outside the flow blocks it (the app will not start, no credentials, the tool is missing), mark it blocked and say why.

Done when every flow from step 1 is passed, failed, or blocked.

## 5. Clean up and report

Close the browser sessions you opened and stop the processes you started. Leave anything you found already running.

Report in the reply, in the user's language:

```markdown
**Result:** 4 passed, 1 failed, 1 blocked. Evidence: /absolute/path/to/evidence

| # | Flow | Tool | Result | Evidence |
|---|---|---|---|---|
| 1 | Sign in with valid credentials | Playwright | ✅ passed | 1-signed-in.png |
| 2 | Save profile with an empty name | Playwright | ❌ failed | 2-no-error.png |

### Failures
**2. Save profile with an empty name**
Steps: open /profile, clear Name, click Save.
Expected: a validation message under Name. Actual: the form saves and the name becomes empty.
Console: `TypeError: cannot read 'trim' of undefined (profile.ts:42)`. Request: `PATCH /api/profile` → 500.

### Blocked
**6. Export to CSV**: no test account with export permission.

### Other findings
Errors seen in flows that passed, and anything not tested and why.
```

Give the evidence directory as an absolute path.

## 6. Offer to codify

Offer to turn the flows that passed with Playwright into `@playwright/test` specs. Computer Use flows cannot be codified; list them as not covered. If the user accepts:

- Follow the project's Playwright setup: its config, test directory, fixtures, `baseURL`, and naming. If the project has no Playwright setup, ask before adding it, since it is a new dependency.
- Build each test from the code the session printed, with role-based locators. Turn each expected outcome into an assertion (`toBeVisible`, `toHaveText`, `toHaveURL`, `toMatchAriaSnapshot`). `generate-locator <ref>` gives the locator for an element.
- One flow per test, each starting from a fresh page. No sleeps and no `networkidle`.
- Run the new specs with `PLAYWRIGHT_HTML_OPEN=never npx playwright test <files>`. Done when they all pass. A test that fails because the app is wrong is a bug for the report, not a test to bend until it passes.
