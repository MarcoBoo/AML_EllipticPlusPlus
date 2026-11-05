# AML on Elliptic++ — which features help to spot illicit Bitcoin transactions?

Project for the **Blockchain and Cryptocurrency** course.

## What it does

The [Elliptic++](https://github.com/git-disl/EllipticPlusPlus) dataset describes 203,769 Bitcoin
transactions, a small part of them labeled licit or illicit, linked in a graph of money flows over
49 time steps. The question of the project is *which groups of features
let a model recognise an illicit transaction**.

To answer it, the project:

- computes 27 **transparent** graph features from the edge list (degrees and ancestor counts,
  centralities, neighbourhood motifs), so that every input has a readable meaning, unlike the
  anonymous features shipped with the dataset;
- builds seven **feature menus** — Elliptic's local features, local + aggregate, graph structure
  only, the economic columns of Elliptic++, all transparent features, everything together, and an
  empty menu where the graph alone speaks;
- tunes and trains eight **models** on each menu (Logistic Regression, Random Forest, XGBoost, MLP,
  GraphSAGE, GATv2, ChebNet, GIN), with a temporal split (train 1–30, validation 31–40, test 41–49),
  three seeds per configuration, and PR-AUC as the main metric;
- compares the menus, then looks **inside** the trained models (permutation importance, SHAP,
  Integrated Gradients, GNNExplainer) to see which families they actually use;
- splits the test results around the **dark-market closure** at time step 43, after which the
  models are known to stop finding illicit transactions.

`Report.pdf` holds the full write-up, the method and the results.

## How it runs

Everything is Jupyter notebooks **meant to run on Google Colab**, with the data on Google Drive:
each notebook mounts Drive, reads a `DATA_PATH` folder, and writes its tables and plots back there,
so the next notebook can pick them up. Runs resume where they stopped, which matters for the long
steps.


## Repository

```
src/     notebooks, one folder per step
data/    raw dataset and all generated tables, parquet files and plots
Report.pdf
```
