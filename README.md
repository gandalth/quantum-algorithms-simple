# Overview

A set of minimal and beginner-friendly implementations
of quantum-computing algorithms based on qiskit.
We use statevectors and require no backend access to a real QPU or a simulator.

Currently implemented:
- Deutsch Algorithm
- Deutsch-Jozsa Algorithm for two-bit input functions
- Bernstein-Vazirani Algorithm
- Phase kickback
- Quantum Fourier Transform (QFT) demonstration (n = 4 / N = 16)
- Quantum Phase Estimation (QPE) for a single qbit
- Amplitude amplification for a single "good state"
- Variational Quantum Eigensolver (VQE) for up to 3 qbits

# Installation

Python and qiskit are required to run the scripts.  Follow IBM's
installation guide on
https://quantum.cloud.ibm.com/docs/en/guides/install-qiskit.

# Algorithms and Usage

## Deutsch Algorithm

The Deutsch Algorithm is the most simple algorithm to demonstrate the
quantum computer's advantage.  It categorizes one-bit-input
one-bit-output functions into two subsets: functions with constant
output (e.g., f(x) = 1) and functions with balanced output (e.g., f(x)
= x).  Given an unknown function as a challenge, a classical computer
has to evaluate the function twice for the categorization
task. Contrary, the Deutsch Algorithm on a quantum computer requires
only one evaluation of the oracle, which is the quantum-equivalent of
the function.

Our implementation lets the user pick a challenge to the algorithm
from these four functions: 'f(x) = 0', 'f(x) = 1', 'f(x) = x', 'f(x) =
not_x'.  The script will prepare the oracle representing the selected
function and the algorithm will evaluate it once. Based on the outcome
it will report "constant output" or "balanced output".

Run the algorithm using
```
python deutsch.py
```

## Deutsch-Jozsa Algorithm for two-bit input functions

The Deutsch-Jozsa Algorithm can be understood as an extension of the
Deutsch Algorithm to functions with multiple input bits. Again, the
algorithm will categorize the function as "constant output" or
"balanced output" with only one evaluation of the oracle function.

Our implementation is currently restricted to two input bits. The user
can choose from the following functions to challenge the algorithm:
'f(x0,x1) = 0', 'f(x0,x1) = 1', 'f(x0,x1) = x0', 'f(x0,x1) = x1',
'f(x0,x1) = not x0', 'f(x0,x1) = not x1', 'f(x0,x1) = x0 xor x1',
'f(x0,x1) = not(x0 xor x1)'.  The script will prepare the oracle
representing the selected function and the algorithm will evaluate it
once. Based on the outcome it will report "constant output" or
"balanced output".

Run the algorithm using
```
python deutsch-jozsa.py
```

## Bernstein-Vazirani Algorithm

The Bernstein-Vazirani Algorithm demonstrates the advantage of quantum
computers by efficiently recovering a secret bitstring s of length
n. It achieves this by evaluating an oracle for the function
XOR_{i=0}^{n-1}(x_i * s_i) exactly once. This is remarkable, as a
classical algorithm would require n evaluations of this function.

Our implementation lets the user enter a secret binary string and
builds the corresponding oracle which is opaque to the
algorithm. After evaluating the oracle once, the algorithm will
recover the correct bitstring.  We suggest to start with strings of 8
bits length and increase the length step by step.

Run the algorithm using
```
python bernstein-vazirani.py
```
## Phase kickback

Phase kickback refers to the effect that, in a controlled unitary
operation, a phase applied to the target qubit can be transferred to
the control qubit if the target is in an eigenstate of that operation.
This allows phase information to be encoded in control qubits and is
used in algorithms such as the Deutsch Algorithm or Bernstein–Vazirani Algorithm.

Our implementation shows the phase applied to the controlling qbit's
states |0> and |1> explicitly. It lets the user choose the function to
be implemented by the unitary from this list: 'f(x) = 0', 'f(x) = 1',
'f(x) = x', 'f(x) = not_x'. The key insight is that the resulting
state reads 1/sqrt(2) * ((-1)^{f(0)}|0> + (-1)^{f(1)}|1>).

Run the algorithm using
```
python phase_kickback.py
```

## Other algorithm descriptions TBD