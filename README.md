# Ionic Liquid Viscosity Prediction

Predicts the viscosity of ionic liquids (cation + anion pair) at a given temperature, using RDKit molecular descriptors and an ensemble of Random Forest, XGBoost and CatBoost.

## Approach

1. Merge ion names with their SMILES strings (`smiles.csv`).
2. Clean data (remove non-physical negative temperatures, drop ions without SMILES).
3. Compute RDKit descriptors per ion, plus cation-anion interaction and `1/T`-coupled features.
4. Benchmark models with 5-fold **GroupKFold** (grouped by ion pair to avoid leakage).
5. Blend predictions: `0.35 CatBoost + 0.35 XGBoost + 0.30 Random Forest`.