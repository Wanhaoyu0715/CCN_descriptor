# Investigation of Surface Passivation Mechanisms in CrCoNi Alloys via Interpretable Machine Learning

## Project Description
This repository contains the code and analysis tools for investigating surface passivation mechanisms in CrCoNi alloys using interpretable machine learning. The project focuses on analyzing atomic structures, coordination number changes, and energy distributions to understand passivation behavior.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Code Structure](#code-structure)
- [Example](#example)

## Installation
Before running the code, ensure the following dependencies are installed:

```bash
pip install ase numpy tqdm
```
## Usage

### Connect to Database
Ensure your database path is correct and connect to the database.

```python
import ase.db
db = ase.db.connect('/path/to/your/db')
rows = db.select()
```
### Run Analysis Script
Run the provided script to analyze atomic structures and calculate coordination number changes.

```python
# Example code
all_atom = []
for row in rows:
    all_atom.append(row)

all_atom = all_atom[:100]
energies = [item.energy for item in all_atom]

# Calculate Cr atom proportions in different height layers
prop1 = [level_proportion(item.toatoms()) for item in all_atom]
prop2 = [mid_proportion(item.toatoms()) for item in all_atom]
prop3 = [btm_proportion(item.toatoms()) for item in all_atom]

# Analyze coordination number changes
cn_matrix = [analyze_coordination(item.toatoms())[0] for item in all_atom]
cn_changes_ratios = [calculate_cn_changes(item.toatoms(), a, b) for item in tqdm(all_atom)]

