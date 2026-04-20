# Overview

A set of minimal and beginner-friendly implementations
of quantum-computing algorithms based on qiskit.
We use statevectors and require no backend access to a real QPU or a simulator.

Currently implemented:
- Deutsch Algorithm
- Deutsch-Jozsa Algorithm for two-bit input functions
- Bernstein-Vazirani Algorithm
- Phase Kickback
- Quantum Fourier Transform (QFT) demonstration (n = 4 / N = 16)
- Quantum Phase Estimation (QPE) for a single qbit
- Amplitude Amplification for a single "good state"
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
## Phase Kickback

Phase kickback refers to the effect that, in a controlled unitary
operation, a phase applied to the target qubit can be transferred to
the control qubit if the target is in an eigenstate of that operation.
This allows phase information to be encoded in control qubits and is
used in algorithms such as the Deutsch Algorithm or Bernstein–Vazirani
Algorithm.

Our implementation shows the phase applied to the controlling qbit's
states |0> and |1> explicitly. It lets the user choose the function to
be implemented by the unitary from this list: 'f(x) = 0', 'f(x) = 1',
'f(x) = x', 'f(x) = not_x'. The key insight is that the resulting
state reads 1/sqrt(2) * ((-1)^{f(0)}|0> + (-1)^{f(1)}|1>).

Run the algorithm using
```
python phase_kickback.py
```

## Quantum Fourier Transformation (QFT)

Quantum Fourier Transformation (QFT) is the quantum analogue of
Discrete Fourier Transformation (DFT). It works on qbits and is of
practical interest due to two reasons: It is used as a component in
many emerging real-world applications, and moreover, it requires lower
complexity than both DFT and Fast Fourier Transformation (FFT).

Our implementation uses n = 4 qbits and lets the user choose from four
input signals to illustrate the basic correspondences of QFT. There
are two signals with amplitude spikes, which will be transformed to a
superposition of uniform amplitude and a phase ramp with constant step
size. The other two possible input signals are uniform superpositions
with a phase ramp of constant step size. These input signals will
result in amplitude spikes at the output of the QFT.

Run the algorithm using
```
python qft.py
```

## Quantum Phase Estimation (QPE)

Similar to QFT, Quantum Phase Estimation (QPE) is an algorithm of high
interest as it serves as a component in many quantum algorithms which
are becoming increasingly popular (e.g. Shor's Algorithm or Quantum
Counting). In essence, QPE is used to estimate the phase associated
with an eigenvalue of a unitary operator by encoding it into a quantum
state and extracting it via interference and measurement. Note: this "uses"
phase kickback as observed before.

In our implementation we choose the controlled-phase operator as a an
easy example of a unitary operator. We prepare the target qbit in |1>
state, which is an eigenstate of this operator. The user can choose
the angle of the operator and can observe how QPE uses the
probabibilites of the controlling qbits state vector to infer the
angle.

Run the algorithm using
```
python qpe_single_qbit.py
```

## Amplitude Amplification

Amplitude Amplification is an iterative search algorithm that
alternates between an oracle, which marks the searched / good states
via a phase flip, and a diffusion operator, which amplifies their
amplitudes by reflecting the state about the average. Assuming only
one good state, this operation can be understood as a rotation towards
that state in sqrt(N) steps, with N being the total number of
states. Compared to classical search algorithms, Amplitude
Amplification provides a quadratic speedup (O(sqrt(N)) over O(N)).

Our implementation uses exactly one good state that the user
defines. It shows the probabilities of the qbit states over the
iterations and stops when the algorithm converges to a specific state
or the maximum number of iterations is reached.

Run the algorithm using
```
python amplitude_amplification.py
```

## Variational Quantum Eigensolver (VQE)

A Variational Quantum Eigensolver (VQE) is a hybrid quantum-classical
algorithm that finds the minimum energy (ground state) of a
Hamiltonian.  It is widely used in applications such as quantum
chemistry and drug discovery. VQE’s potential quantum advantage lies
in using a quantum system to efficiently represent and measure
properties of states that would be exponentially costly to simulate
classically.

Our implementation uses random search and is limited to 3 qubits. We
compute the exact ground state for comparison, track the VQE energy over
iterations, and report the relative error. The Hamiltonian is specified
as a sum of Pauli terms, and depending on whether complex coefficients
are present, we choose either a real-valued ansatz or a complex-valued
extension.

Run the algorithm using
```
python vqe.py
```
