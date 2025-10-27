# Evaluation Methodology

Each DPAI Arena task is evaluated through **two independent trials** designed to measure both **generalization** (how well an AI coding agent performs without prior hints) and **adaptation** (how effectively it refines solutions once the expected tests are known).  
All results are normalized to a **0–100 scale** for consistent comparability across agents, languages, and workflows.  

## Trial 1 — Blind Evaluation
In the first trial, the coding agent receives only the **task description** and **project context**, without access to the hidden target tests.  
This setup simulates how real-world developers approach tasks with incomplete specifications.  

- **Functional Score (0–100):** Measures the proportion of hidden (target) tests passed successfully.  
- **Regression Bonus (0–25):** Rewards agents that preserve existing functionality. All project baseline tests are re-executed, and up to 25 points are awarded proportionally based on how many pass.  
- Both components are combined and normalized to yield the **Trial 1 Score (0–100)**.  

## Trial 2 — Informed Evaluation
In the second trial, the environment is re-executed with a **test patch pre-applied**, giving the agent access to the target tests and allowing it to design its solution accordingly.  
Scoring follows the same structure (functional + regression → normalized to 0–100).  
This measures how well an agent can **adapt and optimize** once evaluation criteria are visible.  

## Final Aggregated Score
To reflect real-world relevance, **Trial 1** (generalization) carries higher weight than **Trial 2** (adaptation).  
The final benchmark score is computed as:  

```
FinalScore = Trial1Score + 0.5 × Trial2Score
```

The combined result is then normalized to a **0–100 scale** to maintain consistency across all tasks.  

## Interpretation
- **Trial 1** → *Generalization:* How well an agent produces correct solutions without seeing validation tests.  
- **Trial 2** → *Adaptation:* How well it fine-tunes output when tests are known.  
- **Regression component** → *Reliability:* Ensures new code doesn’t break existing functionality.  
- The **1 : 0.5 weighting** prioritizes authentic problem-solving while still rewarding learning and stability.  

---

# Mathematical Appendix

## Trial 1 — Blind Evaluation
```
FunctionalScore = 100 × (passed_target_tests / total_target_tests)
RegressionScore = 25 × (passed_baseline_tests / total_baseline_tests)
Trial1Score = 100 × (FunctionalScore + RegressionScore) / 125
```

## Trial 2 — Informed Evaluation
Uses the same formulas as Trial 1.  

## Final Score
```
FinalScore = Trial1Score + 0.5 × Trial2Score
Normalized FinalScore = 100 × (FinalScore / 150)
```

## Example

| Metric | Description | Value |
|---------|--------------|--------|
| Target tests total | 20 | |
| Target tests passed (Trial 1) | 10 | |
| Baseline tests total | 50 | |
| Baseline tests passed (Trial 1) | 50 | |
| Target tests passed (Trial 2) | 18 | |
| Baseline tests passed (Trial 2) | 50 | |

**Step 1 – Trial 1:**  
Functional = 100 × (10 / 20) = 50  
Regression = 25 × (50 / 50) = 25  
Trial 1 = 100 × (50 + 25) / 125 = 60  

**Step 2 – Trial 2:**  
Functional = 100 × (18 / 20) = 90  
Regression = 25 × (50 / 50) = 25  
Trial 2 = 100 × (90 + 25) / 125 = 92  

**Step 3 – Final Score:**  
```
FinalScore = 60 + 0.5 × 92 = 106
Normalized FinalScore = 100 × (106 / 150) = 70.7
```
