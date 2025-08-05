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

## 3. Issue Creation Workflow

To create a new issue suitable for inclusion in the benchmark:

1. **Describe the Problem Clearly**\
   The issue must include a self-contained problem statement that is understandable without requiring external links or explanations. It should define:

   - **The intent** — What functionality or behavior is being introduced or fixed?
   - **Constraints** — Any assumptions, limitations, or required tools/APIs.

2. **Specify Tags**\
   Add the following labels to every issue:

   - Language-specific or technology labels (e.g., `Java`, `Spring`, `Maven`) to support categorization.
   - `Good First Issue` or `Advanced`, depending on complexity.
   - Optional: `Bug`, `Feature`, or `Refactor` to clarify nature.

3. **Prepare for Testing**\
   Ensure the issue can be implemented in a way that conforms to [Section 2. Tests](#2-tests):

   - Must support creation of a **black-box test suite** that fails before and passes after the fix or feature.
   - Must not rely on flaky or external system behavior.
   - Should define expected behavior in terms that can be verified through public interfaces.

4. **Enable Traceability**\
   Use a descriptive issue title and include any relevant file paths or APIs. This helps maintain clear links between the issue, its implementation, and test verification.

## 4. Issue Submission Workflow

1. **Verify issue** to be implemented in the repository. If issue can not be implemnted then add a reason as a comment, add `Wontfix` label and reassign task to task creator.
2. **Fork or branch** the repository.
3. **Implement** the issue including source code and tests.
4. **Commit** using the following message structure (replace angle‑bracketed placeholders):
   ```
   <Task name> #<issue number>

   <Task description>
   ```
5. **Add** FAIL_TO_PASS and PASS_TO_PASS to the issue comment:
   ```
   FAIL_TO_PASS: <Failed tests, now passing after the patch>
   PASS_TO_PASS: <Tests that already passed and still pass>
   ```
6. **Open** a PR against `main` or a feature branch. The PR **must** include the following information:
    - **Title**: `<task‑name>`
    - **Label**: `Review`
    - **Reviewers**: `Review`
    - **Body** *(must follow the template below)*:
      ```
      <Task description or additional context>
      ```
7. **Verify CI** – All tests must pass in GitHub Actions.
8. **Address review** – Amend the PR until a Review team approves.

   - FAIL_TO_PASS and PASS_TO_PASS can be added in issue comments to be included in the dataset.
   - Related commits can be added to the issue by including a comment with format: `Related commit:<commit hash>`
   - Dataset problem statement will be extracted from the issue description.

---

## 5. Review Workflow

The following checklist is executed **after** the contributor has completed the Submission Workflow and the PR is ready for human review.

1. **Open the pull request** assigned to the Review team.
2. **Review implementation details** – Ensure code quality, style, and architectural consistency.
3. **Examine the `FAIL_TO_PASS` and `PASS_TO_PASS` test lists** – Confirm that proposed tests do *not* depend on undocumented implementation details.
4. **Validate commit(s)** – Each commit must address *one* issue, carry the correct message structure, and be linked to its corresponding issue.
5. **Verify compliance with [Acceptance Criteria](https://github.com/jetbrains-eval-lab#7-acceptance-criteria)**.
6. **Apply the `Verified` label** when all checks succeed.
7. **Approve the pull request** – ***Do not*** merge the PR; hand‑off to the Dataset team instead.

---

## 6. Dataset Generation Workflow

Executed **after** the Review team has approved and labeled the pull request.

1. **Create a task‑instance JSON** describing the new benchmark case.
2. **Verify** created dataset item
3. **Close the pull request** once dataset updates are committed to `main`.
4. **Close associated issues** to complete the tracking loop.

---

## 7. Acceptance Criteria

A submission **shall be accepted** when **all** of the following conditions hold:

| # | Criterion                                                                                                                                                                      |
| - | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1 | The task description explicitly states the purpose, problem statement, and measurable success criteria.                                                                        |
| 2 | The automated tests fail (or are absent) before the reference implementation and pass after it.                                                                                |
| 3 | Tests assess behaviour without introspecting implementation details, unless such details are precisely documented.                                                             |
| 4 | All relevant edge cases and error scenarios are covered by tests.                                                                                                              |
| 5 | The commit message follows the prescribed structure and the description portion is identical, verbatim, to the README description.                                             |
| 6 | The pull request bears the label `Review`, adheres to the PR‑body template (including `FAIL_TO_PASS` and `PASS_TO_PASS` sections), and all CI pipelines complete successfully. |
| 7 | Review Workflow steps 1–7 and Dataset Generation Workflow steps 1–6 have been completed.                                                                                       |
| 8 | Any deviations from these policies are duly justified in the PR description and accepted by maintainers.                                                                       |

---

## 8. Best‑Practice Recommendations

- Decompose complex scenarios into multiple focused tasks.
- Use parameterised tests to minimise duplication.
- Provide minimal, runnable examples in the task README.
- Vendor small fixtures instead of downloading data during test execution.

---
