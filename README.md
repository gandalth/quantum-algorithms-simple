# Overview

A set of minimal and beginner-friendly implementations
of quantum-computing algorithms based on qiskit.
We use statevectors and require no backend access to a real QPU or a simulator.

Currently implemented:
- Deutsch Algorithm
- Deutsch-Jozsa Algorithm for two-bit input functions
- Bernstein-Vazirani Algorithm
- Phase-kickback demonstration
- Quantum Fourier Transform (QFT) demonstration (n = 4 / N = 16)
- Quantum Phase Estimation (QPE) for a single qbit
- Amplitude amplification for a single "good state"
- Variational Quantum Eigensolver (VQE) for up to 3 qbits

# Installation

Python and qiskit are required to run the scripts.
Follow IBM's installation guide on https://quantum.cloud.ibm.com/docs/en/guides/install-qiskit.

# Algorithms and Usage

## Deutsch Algorithm

The Deutsch Algorithm is the most simple algorithm to demonstrate an advantage of a quantum computer.
It categorizes one-bit-input one-bit-output functions into two subsets: functions with constant output (e.g., f(x) = 1) and functions with balanced output (e.g., f(x) = x).
Given an unknown function as a challenge, a classical computer requires to evaluate the function twice for the categorization task. Contrary, the Deutsch Algorithm on a quantum computer requires only one evaulation of the oracle, which is the quantum-equivalent of the function.

Our implementation lets the user pick a challenge to the algorithm from these four functions: 'f(x) = 0', 'f(x) = 1', 'f(x) = x', 'f(x) = not_x'.
The script will prepare the oracle representing the selected function and probe it once. Based on the outcome it will report "constant output" or "balanced output".

Run the demo using
```
python deutsch.py
```

## Other algorithm descriptions TBD