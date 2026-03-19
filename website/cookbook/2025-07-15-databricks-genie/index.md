---
title: Evaluating Databricks Genie Spaces
slug: databricks-genie
description: A complete pipeline for tracing, evaluating, and improving a Databricks Genie space using MLflow.
tags: [databricks, genie, evaluation, tracing, genai]
---

[Databricks Genie](https://docs.databricks.com/en/genie/index.html) is a text-to-SQL AI assistant that lets business users ask natural-language questions about their data. A **Genie space** wraps a set of [Unity Catalog](https://docs.databricks.com/en/data-governance/unity-catalog/index.html) tables, text instructions, SQL expressions, and benchmarks that tell Genie how to translate questions into SQL. This cookbook series shows you how to evaluate and improve a Genie space using MLflow.

<!-- truncate -->

## Where MLflow Fits In

MLflow closes the feedback loop on a Genie space:

- **Tracing** -Each Genie conversation becomes an MLflow trace you can inspect, search, and compare in the MLflow UI.
- **Evaluation** -Built-in and custom judges score every trace so you can see exactly which conversations failed and why.
- **Improvement** - Failed traces feed into an LLM that generates copy-paste-ready fixes for the space configuration.

## Pipeline Overview

| Step | Cookbook                                                          | What it does                                                                                                                                          |
| ---- | ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | [Conversation Tracing Pipeline](/cookbook/genie-tracing-pipeline) | Pulls conversations from the Genie SDK and logs each one as an MLflow trace with the question, generated SQL, and response.                           |
| 2    | [Evaluation with LLM Judges](/cookbook/genie-evaluation-judges)   | Runs built-in judges (relevance, safety) and custom Guidelines scorers on the traces to flag quality issues.                                          |
| 3    | [Space Improvement Generator](/cookbook/genie-space-analyzer)     | Loads failed traces, extracts the Genie space config, and generates specific fixes (text instructions, SQL expressions, example queries) with an LLM. |

## Prerequisites

All cookbooks in this series require:

```bash
pip install "mlflow[genai]>=3.10" databricks-sdk openai
```

They run on Databricks and require a [Genie space](https://docs.databricks.com/en/genie/set-up.html). Start with the Tracing Pipeline, then work through Evaluation and the Space Analyzer.
