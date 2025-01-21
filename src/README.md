# Symbolic Regression with Genetic Programming

This project implements symbolic regression using genetic programming principles. The goal is to find a mathematical expression that approximates a given dataset with minimal mean squared error (MSE).

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Features](#features)
- [How It Works](#how-it-works)
- [Requirements](#requirements)
- [Usage](#usage)
- [Key Functions](#key-functions)
- [Results](#results)

## Overview
Symbolic regression is a type of regression analysis that searches for an equation in symbolic form. Instead of pre-defining a model structure, the algorithm discovers both the structure and the parameters of the model.

## Dataset
The dataset is loaded from a `.npz` file and contains:
- `x`: Input features (array)
- `y`: Target values

### Loading the Data
```python
problem = np.load('../data/problem_0.npz')
x = problem['x']
y = problem['y']
```

## Features
- **Random Tree Generation:** Generates random mathematical expressions using predefined functions and input variables.
- **Evaluation:** Computes MSE for a given tree structure compared to the dataset.
- **Genetic Operations:**
  - Mutation: Modifies a random part of the tree.
  - Recombination: Swaps subtrees between two trees.
- **Survivor Selection:** Selects the fittest individuals for the next generation using a tournament-like process.

### Supported Functions (all numpy irreducible functions)
- Arithmetic: `+`, `-`, `*`, `/`
- Trigonometric: `sin`, `cos`, `tan`
- Exponential and Logarithmic: `exp`, `log`
- Others: `sqrt`, `abs`

## How It Works
1. **Initialization:**
   - Generate a population of random mathematical expressions based on input variables and functions.
2. **Evaluation:**
   - Compute the fitness of each individual using Mean Squared Error (MSE) compared to target values.
3. **Selection:**
   - Perform a tournament selection process to choose the fittest individuals for reproduction.
4. **Reproduction:**
   - Create new individuals via mutation (altering parts of trees) and recombination (swapping subtrees between parents).
5. **Replacement:**
   - Form the new population by combining survivors, offspring, and some entirely new individuals.
6. **Iteration:**
   - Repeat the evaluation, selection, reproduction, and replacement steps for a fixed number of generations or until a termination criterion is met.

## Requirements
To run this code, install the following Python packages:
```bash
pip install numpy
```

## Usage
1. Clone the repository and navigate to the project directory.
2. Load the dataset:
   ```python
   problem = np.load('../data/problem_0.npz')
   x = problem['x']
   y = problem['y']
   ```
3. Run the symbolic regression algorithm:
   ```python
   best_tree, best_mse = Sym_reg(x, y, max_depth=7, population_size=1000, generations=100, mutation_rate=0.3)
   ```
4. View the results:
   - Best tree structure
   - Mathematical formula
   - MSE

### Example Output
```
Generation 1/10
Best MSE: 0.452134
...
Generation 10/10
Best Tree: (<ufunc 'add'>, 5, (<ufunc 'sin'>, x[0]))
Best Formula: def f(x): return (5 + np.sin(x[0]))
Best MSE: 0.125673
```

## Key Functions

### `Generate_tree`
Generates a random tree representing a mathematical expression.

### `Convert_tree_to_expression`
Converts a tree into a NumPy-executable formula.

### `Calculate_mse`
Calculates the MSE of a tree's predictions compared to the target values.

### `Mutate_tree`
Randomly modifies a subtree or terminal node in the tree.

### `Recombinate_trees`
Swaps subtrees between two parent trees to create offspring.

### `Sym_reg`
The main function for running symbolic regression. Handles population initialization, evaluation, selection, reproduction, and replacement.

## Results
The algorithm outputs:
- **Best Tree:** The tree structure of the best solution.
- **Best Formula:** The mathematical expression derived from the best tree.
- **Best MSE:** The mean squared error of the best solution.

## Requirements
 - Python 3.7+
 - NumPy



