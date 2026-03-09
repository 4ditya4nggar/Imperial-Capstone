BBO Capstone Dataset Datasheet
Motivation

This dataset was developed to facilitate practical learning and experimentation with Bayesian Black-Box Optimisation (BBO) as part of the capstone project. It allows students to apply surrogate-based optimisation methods to a variety of benchmark functions. The dataset supports several learning objectives, including:

Understanding Gaussian Process modelling and methods for uncertainty estimation

Designing and analysing acquisition functions such as Expected Improvement (EI), Probability of Improvement (PI), and Upper Confidence Bound (UCB)

Exploring different strategies for generating candidate points

Building intuition about the exploration–exploitation balance that underpins optimisation algorithms

Composition

The dataset consists of input–output pairs generated from eight synthetic black-box benchmark functions. Each function maps a continuous input vector to a single scalar output.

Size and format

Dimensionality ranges from 2 to 8 input dimensions, depending on the function

Data are stored in two formats: NumPy binary arrays (.npy) and plain-text log files

File structure:

data/initial_data/function_{id}/initial_inputs.npy

data/initial_data/function_{id}/initial_outputs.npy

data/latest/inputs.txt

data/latest/outputs.txt

The NumPy files contain the initial query points and corresponding outputs provided at the start of the project, while the text files store incremental observations collected during optimisation rounds.

Known limitations

Coverage becomes sparse in higher-dimensional spaces due to the curse of dimensionality

For Function 1, the dataset currently lacks dense sampling near suspected point-source regions (status as of 19/12/2025)

Many potential extrema remain unexplored because only a limited number of queries have been evaluated

Collection Process

Query generation

Data points were generated iteratively using Bayesian optimisation techniques.

Candidate generation

Fixed grid sampling for 2-dimensional problems

Adaptive grid sampling for 3D and 4D spaces

Latin Hypercube Sampling (LHS) with dimension-aware bias for problems with five or more dimensions

Acquisition-based selection
Acquisition metrics such as EI, PI, and UCB were evaluated over candidate points, and the points with the highest acquisition values were selected for evaluation.

Adaptive parameter tuning
The exploration–exploitation balance (controlled by the beta parameter) was adjusted dynamically based on predicted uncertainty and expected improvement thresholds.

Evolution of the Search Strategy

Phase 1
The initial implementation used a Radial Basis Function (RBF) kernel with a fixed Expected Improvement acquisition function. Candidate points were generated using either fixed grids or Latin Hypercube Sampling. In this stage, optimisation relied on a single acquisition metric.

Phase 2
Output values were normalised using StandardScaler, and the Gaussian Process kernel was extended to a Constant + RBF configuration. The number of LHS samples was increased, and kernels were selected manually. Expected Improvement remained the main acquisition strategy, encouraging sampling across uncertain regions.

Phase 3
The codebase was refactored into modular components, including a Utilities.py module that supported a framework for testing eight different kernel configurations. Automatic Relevance Determination (ARD) was used to extract dimension-specific length scales and identify the most influential input dimensions.
Candidate generation also became adaptive: grid sampling was used for problems with fewer than five dimensions, while biased LHS sampling was applied in higher-dimensional cases. Multi-objective tracking was introduced to monitor both minimum and maximum predictions, and the UCB beta parameter was incorporated for exploration control.

Phase 4
Further refinements focused on hyperparameter tuning and computational efficiency. Enhancements included larger LHS sample sets, increased Gaussian Process restarts, and higher grid resolution. Batched predictions were implemented to reduce memory overhead. A portfolio-based acquisition strategy was introduced, evaluating EI, PI, and UCB in parallel instead of sequentially.
An adaptive beta strategy was also added: exploration was increased whenever EI values fell below a predefined threshold or when relative uncertainty was low. High-uncertainty candidates were prioritised while maintaining diversity through distance-based filtering.

Time Frame

Data collection occurred over ten optimisation rounds, corresponding to approximately ten weeks of experimentation.

A total of nine queries were successfully submitted and evaluated

Four additional queries have been proposed but not yet submitted

Preprocessing and Intended Uses

Preprocessing steps

Several preprocessing techniques were applied before modelling:

Input normalisation: Min–Max scaling to the range [0,1]

Output standardisation: zero-mean and unit-variance scaling

Dimensional analysis: ARD methods to determine the relative importance of input dimensions

Intended uses

This dataset is designed primarily for educational and experimental purposes, including:

Developing and testing Gaussian Process surrogate models

Prototyping acquisition functions and candidate generation strategies

Studying uncertainty estimation in optimisation

Experimenting with strategies that balance exploration and exploitation

Inappropriate uses

The dataset should not be used for the following purposes:

Safety-critical systems or medical decision-making

Large-scale benchmarking studies, due to limited data volume

Real-world optimisation tasks without appropriate domain-specific validation

Any assumption that these synthetic functions reflect realistic black-box systems

Distribution and Maintenance

Availability

The dataset is stored in the repository directory:

PCMLAI-Capstone-S2-Public/data/

with the following internal structure:

data/initial_data/ – initial benchmark queries provided by the course instructors

data/latest/ – incremental observations generated during student optimisation rounds

Terms of use

The dataset is intended strictly for educational use within the capstone course. Redistribution outside the course context is not permitted without explicit approval from the course instructors.

Maintenance

Dataset maintenance is performed informally by the course participant. The dataset is updated after each optimisation round by appending new observations to inputs.txt and outputs.txt. No dedicated version control system exists for the dataset itself; instead, its state is tracked through the commit history of the repository.
