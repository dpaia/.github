**Enterprise SWE Benchmark** is an open‑source initiative that curates real‑world software‑engineering tasks to evaluate automated repair, synthesis, and reasoning tools at enterprise scale.

# Task Contribution Policy

This policy defines the mandatory procedure for submitting new benchmarking tasks and their reference implementations for inclusion in the public dataset. Compliance with this policy is a prerequisite for merge approval.

---

## 1. General Principles

1. **Clarity** – Each task **must** be comprehensible without external context.
2. **Reproducibility** – Every task **shall** include an automated test suite that unequivocally demonstrates correctness.
3. **Behaviour‑driven validation** – Tests **shall** verify externally observable behaviour. Reliance on implementation details is forbidden unless those details are explicitly documented.
4. **Traceability** – Commit messages, pull‑request (PR) titles, labels, and directory names **shall** provide an unambiguous audit trail from description → implementation → dataset entry.

---

## 2. Tests

- **Mandatory** – Each submission must contain at least one automated test. The test suite **shall** either fail (if present) or be absent prior to the reference implementation, and **shall** pass once the reference implementation is introduced.
- **Black‑box** – Tests shall exercise only public interfaces (APIs, CLI contracts, file outputs, etc.). Where internal structures must be inspected, such expectations shall be documented in the task description.
- **Deterministic** – Tests must not exhibit flakiness or depend on external services or non‑fixed randomness.
- **Portable** – Tests shall execute via the project’s standard test command (e.g., `pnpm test`, `poetry run pytest`, `mvn test`) within a clean GitHub Actions runner.

---

## 3. Submission Workflow

1. **Fork or branch** the repository.
3. **Implement** the task including source code and tests.
4. **Commit** using the following message structure (replace angle‑bracketed placeholders):
   ```
   <Task name> #<task number>

   <Task description>

   FAIL_TO_PASS: <Failed tests, now passing after the patch>
   PASS_TO_PASS: <Tests that already passed and still pass>
   ```
   **`FAIL_TO_PASS`** and **`PASS_TO_PASS`** suites are automatically executed for every pull request.
5. **Open** a PR against `main`:
   - **Title**: `<task‑name>`
   - **Label**: `Review`
   - **Reviewers**: `Review`
   - **Body** *(must follow the template below)*:
     ```
     <Task description or additional context>

     FAIL_TO_PASS: <Failed tests, now passing after the patch>
     PASS_TO_PASS: <Tests that already passed and still pass>
     ```
     *The same test suites declared here will be executed by CI to verify the patch.*
6. **Verify CI** – All tests must pass in GitHub Actions.
7. **Address review** – Amend the PR until maintainers approve.
8. **Final review** – A reviewer evaluates the implementation, problem statement, and test coverage for policy compliance.
9. **Label removal & closure** – Upon successful review, the `Review` label is removed and the pull request is closed.
10. **Dataset generation** – The merged commit converted into a dataset entry.
11. **Issue housekeeping** – Any linked issues are closed.

---

## 4. Acceptance Criteria

A submission **shall be accepted** when **all** of the following conditions hold:

| # | Criterion                                                                                                                                                                      |
| - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1 | The task description explicitly states the purpose, problem statement, and measurable success criteria.                                                                        |
| 2 | The automated tests fail (or are absent) before the reference implementation and pass after it.                                                                                |
| 3 | Tests assess behaviour without introspecting implementation details, unless such details are precisely documented.                                                             |
| 4 | All relevant edge cases and error scenarios are covered by tests.                                                                                                              |
| 5 | The commit message follows the prescribed structure and the description portion is identical, verbatim, to the README description.                                             |
| 6 | The pull request bears the label `Review`, adheres to the PR‑body template (including `FAIL_TO_PASS` and `PASS_TO_PASS` sections), and all CI pipelines complete successfully. |
| 7 | Steps 7–10 of the Submission Workflow have been completed.                                                                                                                     |
| 8 | Any deviations from these policies are duly justified in the PR description and accepted by maintainers.                                                                       |

---

## 5. Best‑Practice Recommendations

- Decompose complex scenarios into multiple focused tasks.
- Use parameterised tests to minimise duplication.
- Provide minimal, runnable examples in the task README.
- Vendor small fixtures instead of downloading data during test execution.

---
