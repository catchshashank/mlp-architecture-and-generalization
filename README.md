# MLP Architecture and Generalization on MNIST

## Overview
This project studies how **neural network architecture and optimization choices**
affect **generalization, overfitting, and training stability** in multilayer perceptrons (MLPs).

Using the MNIST handwritten digit dataset, I systematically vary:
- network depth and width
- learning rate
- number of training epochs

and analyze their impact on train, validation, and test performance.

The goal is not to maximize accuracy per se, but to understand *why* certain architectures
generalize better than others.

---

## Problem Setting
Neural networks can easily overfit small or moderate datasets.
This project asks:

> How do architectural complexity and optimization hyperparameters jointly determine
> generalization performance?

---

## Methods
- Dataset: MNIST (60,000 train / 10,000 test)
- Models: Feedforward neural networks (1–4 hidden layers)
- Activation: ReLU
- Loss: Categorical cross-entropy
- Optimizer: Adam / SGD
- Evaluation: Train–validation–test splits

### Hyperparameters explored
- **Depth**: 1, 2, 3, 4 layers  
- **Width**: 64, 128, 256, 512 neurons  
- **Learning rate**: 0.001, 0.01, 0.1, 1.0  
- **Epochs**: 10, 20, 40  

---

## Key Findings

### 1. Depth vs Generalization
- Increasing depth improves representational capacity
- Beyond 2–3 layers, **test accuracy drops** due to:
  - vanishing gradients
  - optimization instability
  - overfitting with limited data

### 2. Width vs Overfitting
- Wider layers improve training accuracy monotonically
- Validation and test accuracy saturate beyond ~128 neurons
- Large models show **growing train–test gaps**

### 3. Learning Rate Instability
- Moderate learning rates (≈ 0.001) converge reliably
- High learning rates cause:
  - oscillating loss
  - divergence
  - accuracy collapse

### 4. Epochs and Early Stopping
- More epochs help escape local minima initially
- Excessive training increases overfitting
- Validation-based early stopping improves generalization

---

## Results (Summary)
- Best generalization achieved with **moderate depth and width**
- Test accuracy ≈ **98%**
- Simpler models often outperform deeper networks when data is fixed

This empirically illustrates the **bias–variance tradeoff** and the limits of brute-force scaling.

---

## Why This Matters
This project demonstrates:
- principled model selection
- understanding of optimization dynamics
- diagnosis of overfitting and instability
- translating theory (UAT, bias–variance) into practice

These considerations are central to real-world ML system design.

---

## Reproducibility
All experiments are reproducible via the notebooks in `/notebooks`.

```bash
pip install -r requirements.txt
