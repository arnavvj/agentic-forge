# CLOSE: Acceptance, Handoff, and Readiness

## Objective

Prepare a truthful final status, verify agreed acceptance conditions, document limitations, and hand the project back to the user. This step does not replace the user's final manual testing or acceptance decision.

## 1. Review project scope

- Read `docs/01-PROJECT.md` and the approved plan.
- Review all tasks in `docs/05-TASKS.md`.
- Identify completed, deferred, blocked, and unfinished work.
- Confirm scope changes and important decisions are recorded.

## 2. Verify the implementation

Run checks available and relevant to the project:

- Build / compile
- Formatting and linting
- Type checks
- Unit tests
- Integration tests
- API / contract tests
- End-to-end tests
- Agent evaluations and tool-boundary tests, where applicable
- Dependency or security checks, where available

Report the exact command or method and result. Do not claim unrun checks passed.

## 3. Check the primary user journey

Verify the agreed end-to-end journey as far as the environment allows:

- Does the application start?
- Can the primary user complete the intended journey?
- Are loading, success, empty, and error states handled?
- Do permissions and data boundaries behave as designed?
- Do external integrations work, or are any mocked?
- Can background or durable workflows recover as required?
- Are agent handoffs, tool calls, and human approvals correct where applicable?

Identify checks that require the user to test manually.

## 4. Review security and operational basics

Check applicable requirements: no secrets committed or exposed; authentication and authorization enforced; data boundaries and sensitive-data handling match the design; critical external actions controlled and auditable where required; errors handled deliberately; required logs, health checks, backups, and recovery behavior documented or implemented; dependency, deployment, and configuration requirements recorded.

Do not claim a formal security audit or compliance assessment unless one was actually performed.

## 5. Handoff materials

Ensure the repository includes applicable setup / local run instructions, required environment variables without secret values, build and test commands, deployment notes, integration and mock / sandbox notes, architecture and workflow notes, known limitations, deferred items, and demo instructions.

## 6. Final status report

### Delivered
What is implemented and usable.

### Verification

| Check | Result | Notes |
|---|---|---|
| Build | [ ] Pass [ ] Fail [ ] Not run | |
| Tests | [ ] Pass [ ] Fail [ ] Not run | |
| Primary journey | [ ] Verified [ ] Partial [ ] Not verified | |
| Permissions / safety | [ ] Verified [ ] Partial [ ] Not verified [ ] N/A | |
| Manual user testing | [ ] Complete [ ] Pending | |

### Remaining work
List unfinished tasks, deferred scope, known bugs, and limitations.

### Run and demo instructions
Provide the exact steps needed to start and demonstrate the application.

### Readiness assessment

Select and explain one:
- **Prototype / demo ready:** The agreed demo path works, with limitations stated.
- **MVP ready for user acceptance:** The agreed MVP scope is implemented and verification is documented; user acceptance is still required.
- **Production candidate:** Relevant production requirements have been addressed and evidence is available, but deployment and operational approval may remain.
- **Not ready:** Important acceptance criteria or blockers remain.

Do not label an application production-ready simply because it builds or passes a limited test suite.

## 7. User acceptance

- [ ] User completed required manual tests.
- [ ] User reviewed known limitations.
- [ ] User accepted the delivered scope.
- [ ] Follow-up work has been recorded.

**Final acceptance belongs to the user.**

## Stop condition

Present the handoff report and wait for the user's acceptance or further direction.
