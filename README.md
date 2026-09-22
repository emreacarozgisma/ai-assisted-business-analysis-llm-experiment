# AI-Assisted Business Analysis: LLM Prompting Experiment

This repository contains the public reproducibility materials for the Master's dissertation:

**AI-Assisted Business Analysis: An Empirical Evaluation of LLM-Generated Business Analysis Artifacts Across Prompting Approaches**

## Overview

The study evaluates how different prompting approaches affect the generation of common Business Analysis artifacts in a FinTech/Open Banking context.

The formal experiment used:

- **10 evaluation scenarios**
- **3 artifact types:** User Story, Acceptance Criteria, Business Rules
- **4 prompting approaches:** Zero-shot, Role-based, Structured, Few-shot
- **3 independent generations per condition**

This results in:

**10 × 3 × 4 × 3 = 360 generated outputs**

The generation model used in the formal experiment was **gpt-5.6-terra**. Semantic stability was assessed using **text-embedding-3-large**.

## Repository Contents

```text
/
├── README.md
├── experiment_pipeline_github_ready.ipynb
└── data/
    └── Thesis_Experiment_Public.xlsx
```

### `experiment_pipeline_github_ready.ipynb`

Public version of the research pipeline used to:

- load and validate the public research workbook,
- construct the four prompting conditions,
- generate LLM outputs,
- record efficiency metadata,
- validate the formal experiment structure,
- generate embeddings,
- calculate pairwise cosine similarity and Mean Pairwise Similarity,
- reproduce the dissertation's main inferential statistical comparisons from the aggregated human-evaluation data.

### `data/Thesis_Experiment_Public.xlsx`

Minimal public research workbook containing the materials needed to understand the experiment and reproduce the main analysis pipeline.

The workbook includes:

- scenario cards,
- artifact-specific reference criteria,
- prompt templates,
- few-shot demonstrations,
- the 360-row experiment matrix,
- a blank API-results template for reproduction,
- pairwise semantic-similarity results,
- condition-level aggregated evaluation results,
- statistical-analysis results.

Raw expert-evaluator records and participant-level data are intentionally excluded from the public release. The original 360 generated texts are also not distributed in this workbook.

## Requirements

The notebook is designed to run in **Google Colab** or a compatible Python environment.

The tested Colab installation cell is:

```bash
pip install -q --upgrade openai openpyxl
```

Google Colab already provides commonly used packages required by the notebook, including `pandas`, `numpy`, and `scipy`.

For a local Python environment, install the required packages if they are not already available:

```bash
pip install openai openpyxl pandas numpy scipy
```

## OpenAI API Key

Reproducing the LLM generation or embedding stages requires access to the **OpenAI API** and your own API key.

1. Create or use an OpenAI API account.
2. Create an API key in the OpenAI Platform.
3. Do **not** place the API key directly in the notebook or commit it to GitHub.
4. Provide the key through an environment variable or, when using Google Colab, through **Colab Secrets** using the name:

```text
OPENAI_API_KEY
```

For local execution, the notebook reads the same variable from the environment.

API usage may incur charges according to the OpenAI pricing applicable at the time the notebook is executed.

## Workbook Location

The notebook expects the public workbook at:

```text
data/Thesis_Experiment_Public.xlsx
```

When using Google Colab, create a `data` directory in the current working directory and upload the workbook using that exact filename.

## Safe Default Configuration

API calls are disabled by default:

```python
RUN_GENERATION = False
RUN_EMBEDDINGS = False
```

With both values set to `False`, the workbook-loading, prompt-construction, validation, and statistical-analysis sections can be run without generating new OpenAI API requests.

To reproduce the generation stage, explicitly set:

```python
RUN_GENERATION = True
```

To reproduce the embedding-based stability analysis, explicitly set:

```python
RUN_EMBEDDINGS = True
```

These settings should only be enabled when valid API credentials are configured and the user intentionally wants to make API calls.

## Experimental Configuration

### Generation

- **Model:** `gpt-5.6-terra`
- **Reasoning effort:** low
- **Conversation state:** none
- **API calls:** independent
- **Storage:** `store=False`
- **Generations per condition:** 3
- **Formal outputs:** 360

### Stability

- **Embedding model:** `text-embedding-3-large`
- **Method:** cosine similarity
- **Pairwise comparisons:** Run 1–Run 2, Run 1–Run 3, Run 2–Run 3
- **Condition-level measure:** Mean Pairwise Similarity

Semantic similarity is used as a **stability/repeatability measure**, not as a quality measure.

## Human and Objective Evaluation

Human evaluation was conducted by three professional Business Analysts with FinTech expertise.

The human-evaluation criteria were:

- Completeness
- Correctness
- Clarity
- Consistency
- Testability

The dissertation's primary human outcome is **Mean Human Quality**, calculated at condition level from the five criteria after averaging across the three evaluators.

Objective quality was additionally assessed using scenario- and artifact-specific reference criteria.

Only aggregated evaluation results are included in the public workbook.

## Inferential Statistical Analysis

The public notebook now reproduces the dissertation's main inferential comparisons directly from `13_Evaluation_Summary`.

The analysis uses:

- **Friedman repeated-measures tests** for omnibus comparisons,
- **Kendall's W** as the Friedman effect size,
- **paired Wilcoxon signed-rank tests** for post-hoc pairwise comparisons,
- **Holm adjustment** for multiple comparisons,
- **rank-biserial correlation** as the paired Wilcoxon effect size.

The reproduced comparisons include:

- the overall effect of prompting technique,
- prompting-technique effects within User Stories,
- prompting-technique effects within Acceptance Criteria,
- prompting-technique effects within Business Rules,
- the overall effect of artifact type,
- corresponding pairwise post-hoc comparisons.

The notebook also contains numerical checks against the key Friedman statistics and p-values reported in the dissertation workbook.

### Inter-Rater Reliability

Inter-rater reliability was evaluated using **ICC(2,1)** and **ICC(2,k)**. The dissertation primarily interprets **ICC(2,k)** because the final human-quality measures use the average of three evaluator ratings.

ICC is **not recalculated in the public notebook** because reproducing it requires the evaluator-level ratings. Those records are intentionally excluded from the public release for data-minimisation and privacy reasons.

The resulting ICC statistics are nevertheless reported in:

```text
19_Statistical_Analysis
```

inside the public workbook.

## Efficiency

The experiment recorded:

- latency,
- token consumption,
- estimated API cost.

Condition-level efficiency results are included in the public workbook.

## Reproducibility Scope

This repository is intended to provide sufficient material to understand and reproduce the experimental generation, stability, and main inferential-analysis pipeline while keeping the public release proportionate to the dissertation's research purpose.

The repository does not contain:

- raw participant-level evaluator records,
- personal information,
- internal development/debugging sheets,
- pilot-development history,
- the researcher's private working files,
- the original 360 generated texts.

Exact numerical reproduction of newly generated text is not guaranteed because LLM API outputs may vary across executions and service versions. The repository therefore documents the experimental configuration, prompts, scenario inputs, run matrix, original aggregate results, and analysis procedures used in the dissertation.

## Author

**Emre Acaröz**  
Master's Dissertation  
Data Science, AI and Digital Business  
GISMA University of Applied Sciences

## Citation

If referencing this repository, please cite the associated Master's dissertation and repository URL:

https://github.com/emreacarozgisma/ai-assisted-business-analysis-llm-experiment
