# Developer Productivity AI Arena (DPAI Arena)

DPAI Arena is a curated collection of datasets for benchmarking AI coding agents on real software engineering tasks.
The datasets cover a wide range of software engineering tasks, such as feature implementation, bug fixing, refactoring, test-related work, framework-specific changes, and other scenarios that developers encounter in real projects. Some datasets are created manually, while others are derived from open-source projects and issues.

A key principle behind DPAI Arena is representativeness. Dataset points are reviewed by JetBrains’ product managers, ML engineers and domain experts to ensure they reflect meaningful, realistic developer workflows rather than artificial coding puzzles. 
## Datasets

DPAI Arena datasets are available across repositories in this GitHub organization.

A task is represented as a pull request. The pull request description contains the task statement, while the patch contains the corresponding implementation. Additional metadata, such as test-related information, is included to support evaluation and reproducibility.

This format makes it possible to inspect each task as a real code change: what was requested, what was modified, and what information is available for checking the result.

## Dataset labels

Tasks can be grouped with labels.
Labels may represent task collections, evaluation subsets, technology areas, or other meaningful groupings.  For example, label:default-agent identifies the exact subset of tasks used to select the default agent in JetBrains AI.


## Dataset format

The dataset format describes how dataset points are represented as pull requests, which metadata is expected, and how test-related information should be provided.

Use the [Dataset Format](DATASET_FORMAT.md) document as the source of truth when interpreting dataset points.
