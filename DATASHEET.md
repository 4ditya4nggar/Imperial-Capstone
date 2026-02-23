# Datasheet for the BBO Capstone Dataset

## Motivation
This dataset was created to support a capstone project focused on Bayesian Black-Box Optimisation (BBO) under a constrained evaluation budget. The task is to iteratively select query points for a set of unknown objective functions in order to maximise performance over time. The dataset supports analysis of optimisation behaviour, decision-making under uncertainty, and trade-offs between exploration and exploitation in black-box settings.

## Composition
The dataset consists of sequential optimisation queries and observed outputs across multiple iterations.

- Inputs: Continuous-valued vectors in the range [0, 1], with dimensionality varying from 2D to 8D across eight distinct objective functions.
- Outputs: Scalar objective values returned by each black-box function.
- Size: One query per function per iteration, accumulated over 10+ rounds (continuing until Week 13).
- Format: Numerical arrays (inputs) paired with scalar outputs, logged per iteration.

### Gaps
The dataset is intentionally sparse due to a fixed query budget. Coverage of the input space is uneven, with later iterations concentrated around promising regions.

## Collection Process
Queries were generated iteratively over multiple weeks using an adaptive optimisation strategy. Early rounds focused on broad exploration, middle rounds on identifying patterns (ridges, basins, plateaus), and later rounds on trust-region refinement and stabilisation.

## Preprocessing and Intended Uses
No transformations were applied to inputs or outputs.

### Intended Uses
- Studying optimisation strategies under limited evaluations
- Analysing exploration–exploitation trade-offs
- Teaching and assessment of black-box optimisation concepts

### Inappropriate Uses
- Estimating global optima with statistical guarantees
- Training supervised ML models requiring dense data coverage
- Drawing conclusions about full function landscapes

## Distribution and Maintenance
The dataset is hosted in a public GitHub repository as part of the capstone project. It is intended for academic, non-commercial use and is maintained by the project author.
