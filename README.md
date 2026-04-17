A set of  minimal and beginner-friendly implementations
of quantum algorithms for local use with qiskit.

No backend access to QPU or simulator are needed due to use of statevectors.

Currently implemented:
- Deutsch Algorithm
- Deutsch-Jozsa Algorithm for two-bit input functions
- Bernstein-Vazirani Algorithm
- Phase-kickback demonstration
- Quantum Fourier Transform (QFT) demonstration (n = 4 / N = 16)
- Quantum Phase Estimation (QPE) for a single qbit
- Amplitude amplification for a single "good state"
- Variational Quantum Eigensolver (VQE) for up to 3 qbits

Run using
  python deutsch.py,
  python deutsch-jozsa.py,
  python bernstein-vazirani.py,
  python phase-kickback.py,
  python qft.py
  python qpe_single_qbit.py
  python amplitude_amplification.py
  python vqe.py
in an environment providing qiskit.
