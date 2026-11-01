# CLOSE: Acceptance, Handoff, and Readiness

## Objective

Prepare a truthful final status, verify the agreed acceptance criteria at the depth of the delivery profile, document limitations, and hand the project back to the user. This step does not replace the user's manual testing or acceptance decision.

## 1. Review scope

- Read `docs/01-PROJECT.md` (including the default acceptance criteria), the approved plan, and `docs/05-TASKS.md`.
- Identify completed, deferred, blocked, and unfinished tasks and feedback items.
- Confirm that scope changes and material decisions are recorded.
- Confirm that all accepted work is committed. Report any uncommitted changes. Do not commit them without acceptance.

## 2. Verify the implementation

Run the checks that exist and are relevant: build, formatting and linting, type checks, unit, integration, API / contract, and end-to-end tests, agent evaluations and tool-boundary tests, and dependency or security checks.

Report the exact command or method and its result. Do not claim that unrun checks passed.

## 3. Check the core journey

Verify, as far as the environment allows:

- The application starts, and the primary user can complete the core journey.
- Loading, success, empty, error, and limit-reached states are handled.
- Permissions and data boundaries behave as designed.
- Integrations work, or the mocked ones are listed.
- Background or durable workflows recover as required.
- Agent handoffs, tool calls, limits, and human approvals behave as designed.

List the checks the user must perform manually.

## 4. Security and operations

Check the applicable items: no secrets committed or exposed; authentication and authorization enforced; data boundaries and sensitive-data handling match the design; consequential actions are controlled and auditable where required; errors are handled deliberately; logs, health checks, backups, and recovery are implemented or documented as required.

Do not claim a formal security audit or compliance assessment unless one was actually performed.

## 5. Handoff materials

Make sure the project README or handoff document includes: setup and run instructions, required environment variables (without values), build and test commands, deployment notes, mock and sandbox notes, architecture and agent workflow notes, known limitations, and demo steps.

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
Unfinished tasks, deferred scope, known bugs, and limitations.

### Run and demo instructions
The exact steps to start and demonstrate the application.

### Readiness assessment

Compare the result with the target readiness for the delivery profile in `instructions/00-STANDARDS.md`. Select one and explain:

- **Prototype / demo ready:** The agreed demo path works; limitations are stated.
- **MVP ready for user acceptance:** The agreed MVP scope is implemented and verified; user acceptance is still required.
- **Production candidate:** The production requirements in scope are addressed with evidence; deployment and operational approval may remain.
- **Not ready:** Important acceptance criteria or blockers remain.

Do not call an application production-ready because it builds or passes a limited test suite.

### Hardening gap list

List the gaps between the current state and the next delivery profile (or the current one, if it is not yet met), in priority order, using the profile table in `instructions/00-STANDARDS.md`. If the user wants to continue, this list is the input to `REPLAN`.

## 7. User acceptance

Update "Current state" to Closing, waiting on user acceptance. Final acceptance belongs to the user. When the user accepts, record it in `docs/05-TASKS.md` with a short summary of their message.

## Stop condition

Present the handoff report and wait for the user's acceptance or further direction.
