# Microbiome Environment Classification

This is a learning project I did to explore Databricks and machine learning applications for microbiome data! I built a Random Forest pipeline to classify microbial samples by environment type using 16S rRNA sequencing data. If you'd like a bit more background on the biological side, I've put together a Notion page here (link to come).

## Motivation

I wanted to gain hands-on experience with:
- Databricks ML workflows - how to use the interface, notebook-based pipeline development, and MLflow experiment tracking
- Microbiome data analysis - working with compositional biological data and taxonomic hierarchies
- End-to-end ML pipelines - from raw BIOM files to model evaluation and interpretation

## Project Overview

**Problem:** Given bacterial community composition from an unknown sample, predict which environment it came from.

**Dataset:** 432 samples from this [Qiita microbiome database](https://qiita.ucsd.edu/study/description/13114) across 13 environment types (animal gut, soil, water, sediment, plant surface, etc.)

**Approach:** Random Forest classification on genus-level bacterial abundances with CLR transformation

**Result:** 64.4% accuracy with biologically meaningful features

## Pipeline

1. **Data Ingestion** - Load the BIOM table (31k OTUs) and metadata, aggregate to genus/family level
2. **Preprocessing** - Filter rare taxa (<5% abundance), apply CLR transformation
3. **Feature Engineering** - Use a stratified train/test split due to heavy class imbalance
4. **Model Training** - Random Forest with hyperparameter tuning (RandomizedSearchCV)
5. **Evaluation** - Feature importance and biological interpretation

## Results

**Model Performance:**
- 64.4% test accuracy
- Perfect classification (100%) for sediment and saline water samples
- Struggled with rare classes (<5 test samples)

**Top Bacterial Biomarkers:**
- **Synechococcus** (cyanobacteria) → water environments
- **Methylocystaceae** (methane-oxidizers) → sediment
- **Acetobacteraceae** (plant-associated) → plant/soil samples
- **Enterobacter** (gut bacteria) → animal samples

The model was able to identify bacterial groups that actually do distinguish environments in nature!

## Tech Stack

Databricks, Python, MLflow, scikit-learn, pandas, numpy, biom-format, matplotlib, seaborn

## Limitations & Next Steps

**Current limitations:**
- Small dataset (432 samples) limits generalization
- Some environment types have very few samples
- Only tested Random Forest, could try other models

**Future improvements:**
- Scale to a fuller dataset, e.g., the Earth Microbiome Project dataset (27k samples)
- Deploy as a FastAPI endpoint for predictions given some input microbiome data
- Build a dashboard of some kind (potentially with Streamlit)

## Data Source

Dataset from [Qiita Study 13114](https://qiita.ucsd.edu/study/description/13114)  
Earth Microbiome Project samples across diverse environments

---

**Author:** Thillai Sudhakar  
**Date:** December 2025  
