# ibm_open_science_2021

## Final results
For this solution the decision was to use the Qiskit Pulse for the IBM open science prize 2021 challenge, this module allowed us to explore the possibilities of precise quantum control.

The best achieved fidelity for the full state tomography on the ibmq_jakarta were:
1. **0.8437** fidelity with zero noise extrapolation (fidelity without error mitigation techniques, but including measurement filter was 0.5278). The experiment was run on 20th March 2022 (job id: 623754a3d97bff37d8693572). The circuit was based on:
    * 11 Trotter steps,
    * using RZX based circuit design,
    * having additional calibration runs using qiskit calibration routines,
    * including Carr-Purcel dynamical decoupling sequence with 4 pulses per sequence,
    * with a custom measurement classifier based on k-Nearest Neighbors algorithm and modified amplitudes of default measurement pulses.
    * a measurement filter was applied.
    * Zero noise extrapolation was done based on 6 full tomography scans with different noise scales.

2. **0.8260** and **0.8107** fidelity for a similar circuit as above but run on 26th March 2022 (job id: 623ec33ba2f72d3234dabd1a and 623ec0c974de0e833f85b645). All the settings were the same as above with the exception that no additional calibration routines were run (due to high queue on the machine) and 10 full tomography scans were used for the ZNE.

For the full details of the design circuit and results from other experiments please refer to the included paper.
[IBM open science 2021.pdf](IBM open science 2021.pdf)

<br/>

Many other techniques to improve fidelity were tested but with negative or unclear results, more work and more experiments are needed to fully evaluate other techniques. A short summary of techniques which were not included in the final circuit but described in the full documents are:
* [ 🟩 Promising ] Full benchmark to decide on dynamical decoupling optimal pattern - due to limited hardware availability not enough circuits were run to show the optimal DD pattern (the final solution uses Carr-Purcel sequence).
* [ 🟩 Promising ] Custom pulse schedules for off-resonance and amplitude error reduction (SCROFULOUS, CORPSE, etc.) - some of the results showed improvements of 2-3% for the fidelity, but calibration could be only performed manually and required few additional circuits to be run.
* [ 🟩 Promising ] RZX gate calibration - additional calibration routine for the RZX parameters.
* [ 🟩 Promising ] Qubits frequency calibration - additional calibration routine.
* [ 🟩 Promising ] Probabilistic error cancellation - this technique should provide benefits but with the cost of additional circuits. This technique was not explored for this challenge.
* [ 🟨 Unclear ] Trotter hamiltonian permutations - results on qiskit simulator did not show any improvements.
* [ 🟥 Too expensive ] Piecewise constant optimization for pulse design - this technique requires a very high number of circuits to be run, which was not feasible for this challenge.
* [ ⬜ To specific ] Algorithm mitigation techniques - To apply this technique with improvement to the final fidelity knowledge of the results in need (to choose the perfect trotter steps circuits for the extrapolation).
