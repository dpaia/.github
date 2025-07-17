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

## 3. Issue Submission Workflow

1. **Fork or branch** the repository.
2. **Implement** the issue including source code and tests.
3. **Commit** using the following message structure (replace angle‑bracketed placeholders):
   ```
   <Task name> #<issue number>

   <Task description>

   FAIL_TO_PASS: <Failed tests, now passing after the patch>
   PASS_TO_PASS: <Tests that already passed and still pass>
   ```
   *`FAIL_TO_PASS`* and *`PASS_TO_PASS`* suites are automatically executed for every pull request.*
4. **Open** a PR against `main` or a feature branch. The PR **must** include the following information:
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
5. **Verify CI** – All tests must pass in GitHub Actions.
6. **Address review** – Amend the PR until Review team approve.

---

## 4. Review Workflow

The following checklist is executed **after** the contributor has completed the Submission Workflow and the PR is ready for human review.

1. **Open the pull request** assigned to the Review team.
2. **Review implementation details** – Ensure code quality, style, and architectural consistency.
3. **Examine the `FAIL_TO_PASS` and `PASS_TO_PASS` test lists** – Confirm that proposed tests do *not* depend on undocumented implementation details.
4. **Validate commit(s)** – Each commit must address *one* issue, carry the correct message structure, and be linked to its corresponding issue.
5. **Verify compliance with [Acceptance Criteria](https://github.com/jetbrains-eval-lab#6-acceptance-criteria)**.
6. **Apply the `Verified` label** when all checks succeed.
7. **Approve the pull request** – ***Do not*** merge the PR; hand‑off to the Dataset team instead.

---

## 5. Dataset Generation Workflow

Executed **after** the Review team has approved and labeled the pull request.

1. **Create a task‑instance JSON** describing the new benchmark case.
2. **Append the result JSON** to the appropriate dataset file.
3. **Assign the project** `Enterprise SWE Spring Java Benchmark` to all related issues in the pull request.
4. **Populate the `Dataset` field** in the PR description with the filename(s) of the updated dataset.
5. **Close the pull request** once dataset updates are committed to `main`.
6. **Close associated issues** to complete the tracking loop.

---

### Dataset Format

Each dataset is a JSON file with the following structure:

```json
{
    "instance_id": "owner__repo-pr_number",
    "repo": "owner/repo",
    "base_commit": "commit_hash",
    "problem_statement": "Issue description...",
    "version": "Repository package version",
    "patch": "Gold solution patch (don't look at this if you're trying to solve the problem)",
    "test_patch": "Test patch",
    "created_at": "Date of creation",
    "is_maven": "Is Maven project (true or false)",
    "FAIL_TO_PASS": "Failed tests, but passed after applying the patch or fix",
    "PASS_TO_PASS": "Pass test cases. Shows stability and correctness — the patch did not break existing functionality and may include improvements or refactoring"
}
```

Additional fields may include code embeddings, task metadata, or contextual annotations.

Example:
```json
[
  {
    "instance_id": "example__user__java__project__git-123abc",
    "repo": "example-user/java-enterprise-project.git",
    "base_commit": "abcdef1234567890abcdef1234567890abcdef12",
    "patch": "--- a/src/main/java/com/example/MyService.java\n+++ b/src/main/java/com/example/MyService.java\n@@ -1,4 +1,6 @@\n public class MyService {\n+    private final Logger logger = LoggerFactory.getLogger(MyService.class);\n+\n     public void doWork() {\n         // TODO: implement\n     }\n }",
    "test_patch": "--- a/src/test/java/com/example/MyServiceTest.java\n+++ b/src/test/java/com/example/MyServiceTest.java\n@@ -10,6 +10,10 @@\n     @Test\n     public void testDoWork() {\n         // should log an event\n+        assertDoesNotThrow(() -> myService.doWork());\n     }\n }",
    "problem_statement": "Add logging support to MyService and ensure no exceptions are thrown during doWork() execution.",
    "FAIL_TO_PASS": ["src:com.example.MyServiceTest"],
    "PASS_TO_PASS": [],
    "created_at": "2025-06-25T20:30:00+02:00",
    "version": "0.1",
    "is_maven": "true"
  }
]
```

## 6. Acceptance Criteria

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

## 7. Best‑Practice Recommendations

- Decompose complex scenarios into multiple focused tasks.
- Use parameterised tests to minimise duplication.
- Provide minimal, runnable examples in the task README.
- Vendor small fixtures instead of downloading data during test execution.

---
