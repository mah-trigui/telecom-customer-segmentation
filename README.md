# Telecom Customer Segmentation

A telecom segmentation project showing how unsupervised clustering becomes operationally useful through observation-unit design, variable preparation, iterative profiling, and supervised rule-based assignment.

## Project Website

[View Project Site](https://mah-trigui.github.io/telecom-customer-segmentation/)

## Overview

This project built a full customer segmentation system for telecom CVM operations.

The main difficulty was not the clustering algorithm. It was the design decisions that came before and after clustering:

- defining what one row in the analytical base table should represent
- preparing variables with extreme skewness for distance-based methods
- iterating between clustering and business profiling until segments became actionable
- bridging unsupervised output to a supervised assignment system for new customers

The project had two phases: unsupervised discovery first, then supervised classification to assign new customers using interpretable business rules.

## Core Modeling Pattern

Before asking:

- which clustering method to use

the project first asked:

- what should one row represent — a customer or a behavioral state?
- are the variables even compatible with distance-based clustering?
- do the resulting clusters make operational sense after profiling?
- how do we assign new customers who lack enough history for clustering?

This turns segmentation into a multi-stage system:

1. observation-unit design
2. feature preparation and transformation
3. variable reduction (shape-based + correlation-based)
4. clustering with compression
5. iterative profiling and redesign
6. supervised rule extraction and business threshold adjustment

## Architecture

![Architecture](images/architecture.jpg)

<details>
<summary>📋 View detailed text-based architecture diagram</summary>

```text
  ┌─────────────────────────────────────────────────────┐
  │  PHASE 1: UNSUPERVISED DISCOVERY                    │
  └─────────────────────────────────────────────────────┘

  Raw Behavioral History (recharge, voice, data, mobility, network)
           │
           ▼
  Observation Unit Design
  (one subscriber = one row  OR  one subscriber-month = one row)
           │
           ▼
  Feature Preparation (zero-replacement, capping, per-variable transforms)
           │
           ▼
  Variable Reduction (174 candidates → 49 retained)
           │
           ▼
  Clustering (K-means compression → Hierarchical Ward)
           │
           ▼
  Profiling Loop (represent → cluster → profile → rethink → rebuild)
           │
           ▼
  Operational Segments (Data Addicts, High Consumers, Jeunes, etc.)

  ┌─────────────────────────────────────────────────────┐
  │  PHASE 2: SUPERVISED ASSIGNMENT                     │
  └─────────────────────────────────────────────────────┘

  Decision Tree on Labeled Clusters → Rule Extraction
           │
           ▼
  Business Threshold Adjustment (round, interpret, validate)
           │
           ▼
  Production Assignment (new customers, monthly re-scoring)
```

</details>

## Why this matters

- shows that segmentation begins at representation design, not at the clustering node
- demonstrates that variable shape matters more than variable redundancy for distance-based methods
- treats profiling as part of the method, not as post-hoc cleanup
- bridges unsupervised discovery to production-ready supervised assignment
- generalizes to any behavioral segmentation where clusters must become operational

## Where this pattern generalizes

The same principles apply in:

- banking customers with monthly transaction states
- e-commerce users with lifecycle behavior changes
- subscription products with engagement-state segmentation
- IoT device populations with operating-state clustering
- any domain where unsupervised discovery must translate into production rules

## Public Repository Scope

This public version shares the segmentation architecture, methodological framing, selected pseudocode, and project presentation. Raw telecom data, confidential schemas, and production identifiers are not included.
