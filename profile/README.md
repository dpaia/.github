# DPAI Arena

This is the home of [Developer Productivity AI Arena](https://dpaia.dev/) (DPAIA) and its benchmarks.

DPAI Arena brings measurable productivity into the world of AI-assisted software development. AI tool providers can benchmark and refine their tools on real-world tasks, technology vendors keep their ecosystems first-class by contributing domain-specific benchmarks, enterprises gain a trusted way to evaluate tools before adoption, and developers get transparent insights into what truly boosts productivity.

This repo covers main artefacts for DPAI Arena: projects, datasets, and the harness.

## Projects

**Java \+ Spring.**  *[Bench Score](https://dpaia.dev/#scoreboards)*  
Java \+ Spring benchmark contains 15 open-source Spring-based projects with covering a variety of architectures – from microservices to modular monoliths, to capture the diversity of real-world enterprise development. Benchmark also contains a set of 140+ tasks mirroring realistic enterprise-grade requirements.

## Datasets

The datasets in the Developer Productivity AI Arena are built from real-world project issues, ensuring that each benchmark reflects authentic software engineering challenges. Every datapoint is independently tagged with detailed metadata — such as language, framework, task type, and difficulty level — enabling flexible composition of new, specialized datasets. This modular approach allows contributors to curate domain-specific benchmarks and expand the Arena’s coverage across technologies and workflows.

## CLI Harness (coming soon)

Currently, all DPAI Arena benchmarks run on top of a [dedicated TeamCity instance](https://dpaia.teamcity.com/), ensuring robust orchestration, detailed reporting, and reliable reproducibility.

To further enhance flexibility and openness, we are developing a pipeline-agnostic CLI that will allow anyone to run benchmarks independently of specific CI/CD systems. This open-source tool will enable seamless execution across any environment. *Stay tuned for its release.*

## How evaluation works

Each DPAI Arena task is evaluated through two independent trials designed to measure both generalization (how well an AI coding agent performs without prior hints) and adaptation (how effectively it refines solutions once the expected tests are known).

All results are normalized to a 0–100 scale for consistent comparability across agents, languages, and workflows. Read more about [Evaluation Methodology](EVALUATION.md).

## Benchmarks

We are continuously working on introducing new benchmarks that span **multiple tracks, languages, and frameworks**, reflecting the diverse realities of modern software development. These additions will broaden the scope of the **DPAI Arena**, enabling more comprehensive evaluation of AI coding agents across varied workflows and ecosystems.

A list of available benchmarks, AI agent scores and performance comparisons is published on the [project website](https://dpaia.dev/).

## How to contribute

If you build coding agents, maintain frameworks, or rely on AI-assisted development tools, join the DPAI Arena community. Contribute your tracks, evaluate your agents, and help build a transparent, open foundation for measuring AI-driven developer productivity across languages, workflows, and organizations.

All contribution details, including setup instructions, dataset guidelines, and evaluation workflows, are available in our [Contribution Guidelines](CONTRIBUTION.md). 

