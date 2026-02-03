**# StreamTransformer
Transformer-Based Classification for  Dynamic Data Streams
**Here is a `README.md` file tailored for your project based on the contents of the `ExpermentalCapyMOA_V4.ipynb` notebook.

---

# Transformer-Based Classification for Dynamic Data Streams

**Author:** Ray C. Marange

**Supervisor:** Dr. Heitor Murilo Gomes

**University:** Victoria University of Wellington, NZ

**Year:** 2026

**Project:** AIML 589 Master's Thesis

## Overview

This project implements an experimental evaluation framework for **Online Stream Learning**. The core contribution is a novel **StreamTransformer**—a Transformer-based classifier designed to handle high-throughput data streams. It features a sliding window attention mechanism specifically engineered to adapt to concept drift in real-time.

The framework benchmarks this new model against:

* **Established Streaming Algorithms:** Hoeffding Trees (HT), Extremely Fast Decision Trees (EFDT), Adaptive Random Forests (ARF), and Streaming Random Patches (SRP).
* **Baseline Neural Networks:** A Reactive Multi-Layer Perceptron (MLP).

## Key Features

* **StreamTransformer:** Utilizes PyTorch for deep learning implementation with sinusoidal positional encoding and causal attention masks to process temporal order in streams.
* **Adaptive Resetting:** Includes a `StreamTransformer_ADWIN` wrapper that uses the ADWIN (Adaptive Windowing) drift detector to reset the model's memory upon detecting significant changes in data distribution.
* **CapyMOA Integration:** Leverages the [CapyMOA](https://capymoa.org/) library for efficient stream handling, prequential evaluation, and benchmarking.
* **Automated Pipeline:** An integrated analysis pipeline that performs both drift analysis and prequential evaluation across multiple synthetic and real-world datasets.

## Architecture

The `StreamTransformer` architecture consists of:

1. **Online Standard Scaler:** Implements Welford’s algorithm for incremental normalization of incoming features.
2. **Embedding Layer:** Projects input attributes into a  dimensional space.
3. **Positional Encoding:** Sinusoidal encoding to inject temporal context.
4. **Transformer Encoder:** Multi-layer attention mechanism with a sliding window buffer.
5. **Classification Head:** A linear layer that maps the Transformer output to class probabilities.

## Datasets Supported

The framework evaluates performance on a variety of streams:

* **Synthetic (Drift-heavy):** LED (Abrupt/Gradual), Agrawal (Abrupt/Gradual), and Random RBF Generators.
* **Real-world:** Airlines, Electricity, and Covtype.

## Prerequisites

* Python 3.12+
* Java Runtime Environment (for CapyMOA/MOA backend)
* **Dependencies:**
```bash
pip install capymoa torch numpy pandas matplotlib seaborn tqdm scipy

```



## Usage

1. **Configuration:** Open the notebook and set `TEST_MODE = True` for a quick debug run or `False` for full thesis experiment parameters.
2. **Run Pipeline:** Execute the final cell to start the `INTEGRATED ANALYSIS PIPELINE`.
3. **Outputs:**
* `drift_analysis_results.csv`: Contains drift detection counts from various detectors (ADWIN, PageHinkley, etc.).
* `thesis_results.csv`: Performance metrics (Accuracy, Kappa, Time) for all learners.
* **Visualizations:** Accuracy plots over time/instances are generated automatically for each dataset.



## Results Summary Example (Airlines Dataset)

| Learner | Accuracy (%) | Kappa | Time (s) |
| --- | --- | --- | --- |
| **StreamTransformer** | **69.60** | 27.37 | 350.96 |
| ARF | 68.92 | 25.94 | 907.21 |
| Hoeffding Tree | 67.18 | 19.04 | 30.06 |
| Simple MLP | 63.94 | 12.35 | 89.45 |

*Note: Results extracted from experimental logs within the notebook.*
