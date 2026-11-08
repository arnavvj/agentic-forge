# CLOSE: Acceptance, Handoff, and Readiness

Produce a truthful final status, verify the acceptance criteria at the profile's depth, document limitations, and hand back. This does not replace the user's manual testing or acceptance.

## 1. Scope

- Read `docs/01` (including default acceptance criteria), and `docs/04`.
- Identify completed, deferred, blocked, and unfinished tasks and feedback items.
- Confirm scope changes and material decisions are recorded.
- Confirm all accepted work is committed. Report uncommitted changes; do not commit them without acceptance.

## 2. Verify

Run the relevant existing checks: build, formatting and linting, type checks, unit, integration, API / contract, end-to-end, agent evaluations, tool-boundary tests, dependency and security checks. Report each exact command or method and its result; a check not run is reported as `Not run`.

## 3. Core journey

Verify as far as the environment allows, and list the checks the user must do manually:

- The application starts and the primary user completes the core journey.
- Loading, success, empty, error, and limit-reached states are handled.
- Permissions and data boundaries behave as designed.
- Integrations work, or the mocked ones are listed.
- Background or durable workflows recover as required.
- Agent handoffs, tool calls, limits, and human approvals behave as designed.

## 4. Security and operations

Check as applicable: no secrets committed or exposed; authentication and authorization enforced; data boundaries and sensitive-data handling match the design; consequential actions controlled and auditable where required; errors handled deliberately; logs, health checks, backups, and recovery implemented or documented as required. Do not claim a formal security audit or compliance assessment unless one was performed.

## 5. Handoff materials

The project README or handoff document covers: setup and run, environment variables (names only), build and test commands, deployment notes, mocks and sandboxes, architecture and agent workflow, known limitations, and demo steps.

## 6. Final status report

### Delivered
What is implemented and usable.

### Verification

| Check | Result | Notes |
|---|---|---|
| Build | Pass / Fail / Not run | |
| Tests | Pass / Fail / Not run | |
| Agent evaluations | Pass / Partial / Not run / N/A | |
| Core journey | Verified / Partial / Not verified | |
| Permissions / safety | Verified / Partial / Not verified / N/A | |
| Manual user testing | Complete / Pending | |

### Remaining work
Unfinished tasks, deferred scope, known bugs, limitations.

### Run and demo instructions
Exact steps to start and demonstrate the application.

### Readiness assessment
Compare with the profile's target readiness (`00-STANDARDS.md` section 1). Select one and explain:

- **Prototype / demo ready:** the agreed demo path works; limitations stated.
- **MVP ready for user acceptance:** agreed MVP scope implemented and verified; user acceptance still required.
- **Production candidate:** in-scope production requirements addressed with evidence; deployment and operational approval may remain.
- **Not ready:** important acceptance criteria or blockers remain.

Building or passing a limited test suite does not make an application production-ready.

### Hardening gap list
Gaps between the current state and the next profile (or the current one, if unmet), in priority order, using the profile table in `00-STANDARDS.md`. This is the input to `REPLAN`.

## 7. User acceptance and stop

Set "Now" to Closing, waiting on user acceptance. Present the report and wait. Final acceptance belongs to the user; when given, record it in `docs/04` (`CLAUDE.md` section 5).
