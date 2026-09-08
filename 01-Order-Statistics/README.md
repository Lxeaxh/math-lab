# Math Lab

A personal learning repository for developing a deeper understanding of mathematics, statistics, and machine learning through mathematical reasoning, Python experiments, and clear interpretation.

Rather than treating mathematics as a collection of formulas to memorize, this repository focuses on understanding **why mathematical ideas work**, testing them with examples or simulations, and explaining the results clearly.

## Purpose

The main goals of this repository are to:

* build a deeper understanding of mathematics and statistics;
* connect mathematical theory with Python implementation;
* practice the typical reasoning process used in data science;
* verify theoretical results through computation, visualization, or simulation when appropriate;
* improve my ability to explain technical ideas clearly;
* build reproducible notebooks that show both my reasoning process and technical development.

The purpose is not to make each notebook unnecessarily complicated.

Instead, I focus on the following process:

**Question → Reasoning → Experiment → Evidence → Interpretation**

When appropriate, I also use a broader data science workflow:

**Question → Hypothesis → Data / Example → Exploration → Method → Result → Validation → Interpretation**

## Approach

Each notebook begins with a specific question or point of confusion.

I first identify what I do and do not understand, and then choose an investigation method that fits the question.

Depending on the topic, this may include:

* mathematical derivation;
* hand calculations;
* small concrete examples;
* visualization;
* simulation;
* Python implementation;
* comparison with standard libraries;
* theoretical vs. empirical validation.

The method is chosen based on what helps answer the question rather than to make the notebook look technically complex.

## Notebook Style

Most notebooks follow a structure similar to:

### Goal / Question

What do I want to understand?

### Confusion Map

What was unclear before starting the investigation?

### Minimal Background

Only the definitions, formulas, and assumptions needed for the investigation.

### Investigation

A focused mathematical or computational investigation.

This may contain:

* a hypothesis;
* a concrete example;
* a calculation;
* Python code;
* a visualization;
* a simulation.

### Results / Findings

What did the calculation or experiment show?

### Interpretation

Why did the result occur, and what does it mean mathematically?

### What Changed in My Understanding

How is my understanding different from before the investigation?

### Remaining Questions

What would be worth investigating next?

Not every notebook needs every section. The important part is maintaining the flow:

**Question → Evidence → Interpretation**

## Current Investigations

### Order Statistics

The first notebook investigates the connection between order statistics and counting.

The main question is why an event involving the r-th smallest observation can be rewritten as a statement about how many original observations fall below a threshold.

The investigation includes:

* order statistics and ranking;
* the difference between “exactly” and “at least”;
* the connection between order statistics and the Binomial distribution;
* converting a PDF into a CDF;
* hand calculation of an order-statistic probability;
* visualization of observations relative to a threshold;
* from-scratch Python calculation;
* comparison with SciPy;
* simulation-based validation.

The main conceptual lesson is that **ranking and counting can provide two different descriptions of the same event**.

## Repository Structure

The repository intentionally starts with a minimal structure.

```text
math-lab/
├── README.md
└── order_statistics.ipynb
```

I do not organize notebooks into predefined categories such as `probability/`, `statistics/`, or `machine-learning/` before they are needed.

New folders, Python files, datasets, or reusable utilities will be added only when actual projects create a reason for them.

The repository structure therefore grows with the work rather than being designed in advance.

## Tools

The main tools used in this repository include:

* Python
* NumPy
* pandas
* Matplotlib
* SciPy
* Jupyter Notebook
* VS Code
* Git
* GitHub

Additional libraries will be introduced only when they are useful for a specific investigation.

## What I Am Practicing

Through these notebooks, I am practicing both mathematical and data science skills, including:

* translating mathematical questions into testable problems;
* forming hypotheses before looking at results;
* connecting formulas with their underlying meaning;
* implementing mathematical ideas in Python;
* interpreting computational outputs;
* designing useful visualizations;
* using simulation to test theoretical claims;
* comparing theoretical and empirical results;
* validating from-scratch calculations with standard libraries;
* separating results from interpretation;
* communicating technical reasoning clearly.

## Development Philosophy

This repository is a learning environment, so some notebooks may begin with basic questions.

Those questions are intentionally documented because identifying and resolving misunderstandings is part of the learning process.

The goal is not to demonstrate that every concept was already understood.

The goal is to demonstrate the ability to:

1. identify a precise question;
2. reason about it mathematically;
3. choose an appropriate investigation method;
4. test the idea;
5. evaluate the evidence;
6. explain what the result means.

Over time, the notebooks should show growth in both mathematical understanding and technical problem-solving ability.
