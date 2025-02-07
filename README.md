# Quantum Circuit Fidelity Benchmarking

This repository contains a comprehensive framework for simulating quantum circuits under depolarizing noise and applying fidelity optimization techniques for fidelity correction and optimization.

## Framework Includes:
- Quantum Circuit Simulation using Cirq
- Depolarizing Noise Modelling for NISQ-era quantum devices
- Error Mitigation Techniques: Deterministic, Stochastic, Bayesian Optimization
- Machine Learning-based Fidelity Enhancement using TensorFlow
- Reinforcement Learning (PPO-based) for Adaptive Optimization
- Variational Models for parameterized quantum error correction

---

## Getting Started

### 1. Open the Google Colab Notebook
https://colab.research.google.com/drive/1oE71SeZeaZ03FLcmhx7kDK2NWJeAVBC3

### 2. Install Dependencies
```bash
pip install cirq tqdm tensorflow bayesian-optimization stable-baselines3 shimmy gym
```

### 3. Run the Notebook
- Execute the quantum circuit simulation.
- Apply ML-based fidelity correction techniques.
- Compare performance across noise levels.

---

## Key Features

### Quantum Circuit Simulation
- Randomized Rx circuits initialized with Hadamard gates.
- CNOT entanglement layers for generating correlations.
- Depolarizing noise channel applied at each layer.

### Fidelity Benchmarking
We define a statistical fidelity metric:

\[ F = e^{-\eta} \frac{(p + C)}{2} \]

where:
- p = Probability of measuring ‘1’ outcomes
- C = Mean absolute correlation between adjacent qubits
- e^{-\eta} = Exponential noise decay factor

This metric is computationally efficient and strongly correlates with conventional fidelity measures like Uhlmann fidelity and Trace Distance.

### Fidelity Enhancement Methods

| Method | Description |
|--------|-------------|
| Deterministic Correction | Simple heuristic-based correction for low-noise conditions. |
| Stochastic Sampling | Monte Carlo-based fidelity estimation using small perturbations. |
| Bayesian Optimization | Gaussian Process-based search for optimal correction parameters. |
| Gradient-Based Optimization (TF) | TensorFlow-powered dynamic correction with backpropagation. |
| Reinforcement Learning (PPO) | RL agent learns optimal fidelity-enhancing actions. |
| Variational Model (Single Parameter) | Trigonometric correction model optimizing a single parameter θ. |
| Neural Variational Model | Neural network learns fidelity correction for arbitrary configurations. |

---

## Benchmarking Results

- Baseline Fidelity (No Correction): ~0.25 in noiseless conditions.
- Best Achieved Fidelity: 0.45+ using Reinforcement Learning & Variational Models.
- Performance Hierarchy: RL > Variational > Bayesian > Gradient-based > Stochastic > Deterministic.
- Higher Noise → Diminishing returns for all methods.

### Benchmarking Figure

![Fig](https://github.com/user-attachments/assets/148c8b32-b6ae-470c-91f6-20f4459966b1)
--

## Methodological Details

### Circuit Generation & Noise Model
- Qubits initialized to |0⟩ and evolved through Rx rotations + CNOT layers.
- Depolarizing Noise Model:

  \[ E(\rho) = (1-\eta)\rho + \eta \frac{I}{2} \]

- Measurements performed across 100 shots per circuit.

### Machine Learning Pipeline
- Input Features: Probability of ‘1’ outcomes, mean qubit correlation, noise level.
- Output: Corrected fidelity after optimization.
- Optimization Criteria:

  \[ \text{Optimize } (p + C) / 2 \text{ under constraints} \]

### Reinforcement Learning Agent (PPO)
- State Space: (p, C, noise level)
- Action Space: (Δp, ΔC) small corrections applied to improve fidelity.
- Reward Function:

  \[ R = e^{-\eta} \frac{(p + \delta p) + (C + \delta C)}{2} \]

- Training Strategy: PPO with advantage function estimation.

### Variational Models
- Single-Parameter Model: Uses sinusoidal variations for smooth corrections.
- Neural Network Model: Learns global corrections over circuit configurations.

---

## Future Directions
- Extending to larger grids & real hardware validation.
- Integrating phase-sensitive corrections for coherent noise models.
- Testing advanced RL policies (SAC, TRPO) & quantum-aware optimizations.

---

## How to Cite This Work
If you use this repository in your research, please cite:

Apostolos Panagiotopoulos, *Quantum Circuit Classical Simulation and Fidelity Benchmarking*, 2025.

Full Report: [cirqQuantumCircuitFidelityBenchmark.pdf](./cirqQuantumCircuitFidelityBenchmark.pdf)

---

## Tags & Technologies
- `quantum-computing`
- `cirq`
- `tensorflow`
- `bayesian-optimization`
- `reinforcement-learning`

---

### Author & Contact
Apostolos Panagiotopoulos  
[apostolospanas@gmail.com](mailto:apostolospanas@gmail.com)  

If you find this work useful, star this repository on GitHub!

MIT License

Copyright (c) 2025 Apostolos Panagiotopoulos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
