# Replication code for "Demographic influences on investment: a causal discovery study in Japan"


This repository contains the Jupyter notebooks used for the empirical and simulation analyses in the manuscript. The empirical analyses use the 2022 Preference Parameter Study, Japan Household Panel Survey on Consumer Preferences and Satisfaction (JHPS-CPS), and apply FCI with KCI-based conditional independence testing to mixed continuous/discrete variables.

The individual-level data are not included in this repository. See [Data Availability Statement](#data-availability-statement) below.

## Repository contents

| File | Purpose |
|---|---|
| `Demographic_revision-bootstrap-100_1.ipynb` | Main empirical FCI analysis using the JHPS-CPS data, including preprocessing, variable construction, background knowledge, and 100 bootstrap FCI runs. |
| `Demographic_revision-MI.ipynb` | Multiple-imputation robustness analysis for the empirical JHPS-CPS analysis. |
| `Encoding_robustness.ipynb` | Robustness check for the encoding of ordinal socioeconomic variables, comparing midpoint, rank-based, and log-midpoint encodings. |
| `CI_benchmark.ipynb` | Synthetic conditional-independence benchmark comparing modified mixed-data KCI with standard KCI after one-hot encoding. |
| `FCI_graph_benchmark.ipynb` | Synthetic graph-level FCI benchmark comparing modified mixed-data KCI with standard KCI after one-hot encoding. |

## Environment

The notebooks are Jupyter notebooks written in Python. The following Python interpreter versions were used:

| Notebook | Python version in notebook metadata |
|---|---|
| `Demographic_revision-bootstrap-100_1.ipynb` | Python 3.11.5 |
| `Demographic_revision-MI.ipynb` | Python 3.11.5 |
| `Encoding_robustness.ipynb` | Python 3.12.3 |
| `CI_benchmark.ipynb` | Python 3.12.3 |
| `FCI_graph_benchmark.ipynb` | Python 3.12.3 |

A recent Python 3.11 or 3.12 environment is recommended.

### Main Python packages

The notebooks use the following packages:

```text
jupyter
numpy
pandas
scipy
scikit-learn
statsmodels
matplotlib
seaborn
networkx
pydot
graphviz
causal-learn
```

Some notebooks require a modified version of `causal-learn` that supports mixed-data KCI through the `is_discrete` argument. In those environments, install the modified fork used in the notebooks:

```bash
pip install git+https://github.com/cdt15/causal-learn.git
```

For the one-hot benchmark baseline, use the upstream `causal-learn` environment instead:

```bash
pip install causal-learn
```

Because the benchmark notebooks compare two implementations, they should be run twice, once in the modified mixed-data KCI environment and once in the upstream one-hot baseline environment.

A minimal setup is:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install jupyter numpy pandas scipy scikit-learn statsmodels matplotlib seaborn networkx pydot graphviz
pip install git+https://github.com/cdt15/causal-learn.git
```


## Data

The empirical notebooks expect the raw JHPS-CPS data file to be placed in the repository root with the following filename:

```text
import_2022.csv
```

The notebooks that require this file are:

```text
Demographic_revision-bootstrap-100_1.ipynb
Demographic_revision-MI.ipynb
Encoding_robustness.ipynb
```

The benchmark notebooks use simulated data and do not require the raw JHPS-CPS file:

```text
CI_benchmark.ipynb
FCI_graph_benchmark.ipynb
```


## Data Availability Statement

This study uses data from the 2022 Preference Parameter Study, Japan Household Panel Survey on Consumer Preferences and Satisfaction (JHPS-CPS), conducted by The University of Osaka. The individual-level data are available for academic research upon application to the Secretariat for the Preference Parameters Study (Institute of Social and Economic Research, The University of Osaka). Applicants must submit the required application form by e-mail or postal mail. Upon approval, access to the data download site is provided by e-mail. Further information is available at: [Japan Household Panel Survey on Consumer Preferences and Satisfaction (JHPS-CPS)](https://www.iser.osaka-u.ac.jp/en/research/opendata).


## Reproducibility notes

- The empirical notebooks require access to the restricted-use JHPS-CPS individual-level data.
- The benchmark notebooks generate synthetic data internally.
- The CI and FCI benchmark notebooks require separate runs for the modified mixed-data KCI method and the one-hot baseline method.

