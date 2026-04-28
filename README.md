# Bell-State Measurement Simulator

Educational simulator for Bell-state measurement as a prelude to entanglement swapping and quantum networking.

This repository contains a simple Jupyter-based activity. A user selects one of the four Bell states, runs the Bell-state measurement transformation, measures both qubits, and sees that the two-bit result identifies the selected Bell state with 100% certainty.

The simulator is designed to reduce the entry barrier for learners before introducing the full entanglement swapping protocol.

## Purpose

Bell-state measurement is a core operation in quantum information science. It appears in quantum teleportation, entanglement swapping, quantum repeaters, distributed quantum computing, and quantum networking.

However, Bell-state measurement can be difficult for students because it combines several ideas at once:

* two-qubit tensor-product states
* entanglement
* Bell states
* basis changes
* CNOT and Hadamard gates
* measurement probabilities
* classical interpretation of a quantum measurement result

This simulator isolates the basic measurement logic.

The main idea is:

Bell-state measurement = inverse Bell-state preparation + computational-basis measurement.

For a standalone Bell state, the result is a two-bit label that identifies the input Bell state.

## Bell states

The four Bell states are:

Phi+ = (|00> + |11>) / sqrt(2)

Phi- = (|00> - |11>) / sqrt(2)

Psi+ = (|01> + |10>) / sqrt(2)

Psi- = (|01> - |10>) / sqrt(2)

These states are maximally entangled two-qubit states. Their information is not stored in either qubit alone. Instead, the important information is stored in the joint correlations and relative phases of the two-qubit state.

For example, in Phi+, measuring both qubits in the computational basis gives either 00 or 11. The outcomes are perfectly correlated. But Phi+ is not simply a classical mixture of 00 and 11. It is a coherent quantum superposition.

This is why Bell states are useful resources for quantum communication and quantum networking.

## Bell-state measurement logic

The Bell-state preparation circuit starts from a computational-basis state, applies a Hadamard gate to the first qubit, and then applies a CNOT gate with the first qubit as control and the second qubit as target.

The Bell-state measurement runs this logic backward:

1. Apply CNOT.
2. Apply H on the first qubit.
3. Measure both qubits in the computational basis.

The simulator uses the following deterministic mapping:

|Input Bell state|State after inverse Bell circuit|Measured bitstring|
|-|-|-|
|Phi+|00|00|
|Phi-|10|10|
|Psi+|01|01|
|Psi-|11|11|

Because the four Bell states are orthogonal and map to four different computational-basis states, the measurement result identifies the input Bell state with 100% certainty.

## Connection to entanglement swapping

This simulator is intended as the first step toward a full entanglement swapping simulator.

In entanglement swapping, two entangled pairs are prepared first:

* qubits 1 and 2 are entangled
* qubits 3 and 4 are entangled

A Bell-state measurement is then performed on the middle qubits, 2 and 3.

The result projects the outer qubits, 1 and 4, into an entangled state. The Bell-state measurement outcome tells the outer parties which Bell state they share.

This classical measurement outcome is essential. Without it, the outer parties do not know which Bell state was created. This is why entanglement swapping does not violate special relativity: usable information still requires classical communication.

## Repository contents

Suggested repository structure:

```text
.
├── README.md
├── sim\\\\\\\_bsm.ipynb
├── sim\\\\\\\_bsm\\\\\\\_educational\\\\\\\_brief.tex
```

The notebook contains the simulator. The LaTeX file contains the educational brief, guided exercises, pre- and post-questions, assessment, and answer key.

## Notebook structure

The notebook is organized into two main cells.

### Cell 1: Tools

This cell defines:

* computational basis states
* Bell states
* Hadamard gate
* Pauli X gate
* CNOT gate
* Bell-state measurement transformation
* measurement probabilities
* Bell-state lookup table
* text formatting helpers

### Cell 2: User interface and graphics

This cell provides an interactive user interface using ipywidgets.

The user selects one of the four Bell states and clicks Run BSM.

The output shows:

* selected Bell state
* input state
* state after CNOT
* state after H on the first qubit
* measurement probabilities
* measured bitstring
* identified Bell state
* conclusion statement
* compact probability graphics

The graphics update when the selected Bell state changes and the simulator is rerun.

## Requirements

The simulator uses a minimal Python stack:

```text
numpy
matplotlib
ipywidgets
jupyter
```

Install dependencies with:

```bash
pip install numpy matplotlib ipywidgets jupyter
```

Then start Jupyter:

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

## Quick start

1. Clone the repository.

```bash
git clone <repository-url>
cd <repository-name>
```

2. Install dependencies.

```bash
pip install numpy matplotlib ipywidgets jupyter
```

3. Open the notebook.

```bash
jupyter notebook
```

4. Run Cell 1.
5. Run Cell 2.
6. Select a Bell state and click Run BSM.

## Expected output

For each input Bell state, the simulator should return a deterministic bitstring.

|Selected input|Measured bitstring|Identified Bell state|
|-|-|-|
|Phi+|00|Phi+|
|Phi-|10|Phi-|
|Psi+|01|Psi+|
|Psi-|11|Psi-|

The probability plot should show probability 1.0 for the correct bitstring and probability 0.0 for the other three bitstrings.

The full Bell-state measurement map should show a one-to-one mapping between Bell-state inputs and computational-basis measurement outputs.

## Educational goals

After using the simulator, learners should be able to:

* write the four Bell states
* explain why Bell states are entangled
* describe the difference between product states and entangled states
* explain why ordinary computational-basis measurement does not distinguish all Bell states
* describe Bell-state measurement as the inverse of Bell-state preparation
* interpret the two-bit measurement result as a Bell-state label
* explain why this label is needed in entanglement swapping
* explain why classical communication is still required in quantum networking protocols

## Teaching sequence

A suggested teaching sequence is:

1. Review single-qubit basis states.
2. Build two-qubit computational-basis states.
3. Introduce Bell states.
4. Explain entanglement as non-factorability of the joint state.
5. Show Bell-state preparation using H and CNOT.
6. Reverse the preparation circuit to obtain Bell-state measurement.
7. Run the simulator for all four Bell states.
8. Connect the two-bit result to entanglement swapping.
9. Discuss why classical communication is required.

## Key teaching points

* Bell states are entangled states.
* Entangled states cannot be written as products of independent single-qubit states.
* Bell-state information is stored in joint correlations and relative phases.
* Measuring each qubit directly is not enough to distinguish all Bell states.
* Bell-state measurement changes basis before measurement.
* The BSM result is a two-bit classical label.
* In entanglement swapping, this label identifies the outer entangled state.
* The classical label must be communicated through an ordinary classical channel.

## Possible extensions

This simulator can be extended into:

* a four-qubit entanglement swapping simulator
* a quantum teleportation simulator
* a noisy Bell-state measurement simulator
* a partial Bell-state analyzer for photonic implementations
* a quantum repeater teaching module
* a classroom worksheet with guided calculations
* an assessment notebook with randomized Bell-state inputs

## License

Choose a license appropriate for your use case.

For code, a permissive license such as MIT is often suitable.

For educational text, figures, and classroom materials, a Creative Commons license may be appropriate.

## Attribution

This simulator and educational brief were developed as part of an instructional sequence on Bell-state measurement, entanglement swapping, and quantum networking.

