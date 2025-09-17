# Architecting Large-Scale Quantum Computers Using a Full-Stack Quantum Computer Simulator

-   민동문 (Prof Dongmoon Min)
- dongmoon.min@skku.edu

## Introduction

`We're a computer architect. We make "real" computer systems!`

-   Processors
-   GPU
-   Deep Learning Accelerators
-   Datacenters
-   Quantum Computers

### How to make the "real" system?

-   Simulator (C/C++)

    -   Software consists of <u>millions of code lines</u> written in C/C++
    -   Runs applications and reports performance & power
    -   Derive the **"best configuration"** of target systems

-   Prototyping (Verilog)
    -   Verilog is the language describing the behavoir of systems
    -   We can use Verilog code for simulation and chip fabrication

`C/C++ -> Verilog -> Packaging`

### Architects are the best engineers

```
Computer architect makes the important design decision
```

-   They know "everything"
    -   Application
    -   Operating System
    -   HW Architecture
    -   VLSI circuits
-   They can do "everything"
    -   Assembly programming
    -   C/C++ programming
    -   Verilog programming

`Every company wants to hire computer architects`

```
Annual salary of architects (fresh Ph.D.): $180,000+ /year
Major companies pay more: $300,000+ /year
Even grad.interns make $10,000+ /month
```

### Successful computer architects

-   Jensen Huang, CEO @ NVIDIA
-   John Hennessy, Ex-Chair @ Stanford, President @ Alphabet (Google)
-   Jim Keller, Lead architect @ AMD, Tesla

### My prior research

1. Quantum / Cryogenic Computer System
    - Cryogenic CMOS modeling for scalable quantum computers
    - Full-stack quantum computer system design
2. Conventional Computer Architecture (e.g., Processor, DRAM)
3. Deep Learning Accelerator & System
4. Datacenter Cost/Performance Analysis & Modeling

`this presentation will mainly focus on topic #1: Quantum Computers`

### Research summary

-   research covers full-stack quantum computers
    -   Application
    -   Quantum Compiler
    -   Quantum Control Processor
    -   Quantum Classical Interface
    -   Qubits
-   Goal: A million-qubit scale fault-tolerant quantum computer

1. Build a full-stack quantum computer simulator
2. Build applications to validate the simulator
3. Optimize full stack while running applications

## Quantum Computer systems

-   This presentation focuses on:
    1. Current & future of quantum computer systems
    2. Quantum computer research of computer / system architects

## Contents

-   Motivation of Developing Large-Scale Quantum Computers
    - Trend of quantum computer research
    - Fault-tolerant quantum computing (FTQC)
-   Architecting Large-Scale Quantum Computer Systems
    - Challenges in Developing Large Scale Quantum Computers
    - Scalability Analysis Tool & Validation
    - A million Qubit Scale Quantum Computer System Design
-   Presentation Summary

## Motivation of Developing Large-Scale Quantum Computers

### Potential of quantum computers

-   Quantum computing is promising for various area!

### Requirement to run quantum algorithms

1. thousands of qubits
2. noiseless gate operations and qubits

### Huge errors

-   error-prone due to:
    1. Decoherence
        - Qubit loses its data over time
            - within $100 \mu s$
    2. Gate error
        - Qubit loses its data with gate operations
        - Cannot run more than 200 operations!

### Trend of quantum computer research

-   Two major approaches in handling the errors: NISQ and FTQC

|          | NISQ (Noisy Intermediate Scale Quantum)                                     | FTQC (Fault-Tolerant Quantum Computing)                                             |
| -------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Concept  | Find applications usable now                                                | Remove errors with error correction                                                 |
| Research | **Application**: Applications using fewer gates (e.g., VQA, VQE, QAOA, QML) | **System**: Scalable FTQC systems (e.g., compiler, error decoder, qubit controller) |

``Professor focuses on FTQC``

### Fault-tolerant quantum computing (FTQC)
- FTQC can resolve the error problem of quantum computers
- Concept:
    - make noiseless logical qubits by using 1000s of noisy physical qubits
1. error occurs in the physical qubits
2. FTQC regularly applies the Error syndrome measurement (ESM) to qubits to get the hint of error time and location
3. error decoder (EDU) finds exact location of error
4. EDU applies error correction to mitigate the error

- this reduces to $>10^{10}$ times lower error

- Major industries (e.g., IBM, Google) also pursue FTQC

#### Requirement of FTQC
- Millions of qubits
    - $>1000$ of noiseless logical qubits
    - $>1000$ of noisy physical qubits

## Architecting Large-Scale Quantum Computer Systems
### Full-Stack fault-tolerant quantum computers (FTQC)
- consists of quantum compiler, quantum control processor(QCP), and quantum-classical interface (QCI)

- Quantum Compiler (Software)
    - complies input application to a multi-level operation
- Quantum Control Processor(Hardware)
    - converts the logical qubit operations to the physical qubit level operations
    - while running the qunatum error correction
- Quantum Classical Interface (Hardware)
    - applies physical qubit level operation by applying appropriate control microwave to qubits

### Various Efforts to design FTQC systems
- Various system designs according to:
    1. Location of QCP & QCI
    2. Type of wires

#### Trend 1
- Widely used design:
    - 300Kelvin
    - hardware is in room temperature
    - transfer microwave to qubits using coaxical cables

- Google Sycamore (with 49 qubits)
    - QCP, QCI in room temperature
    - temperature goes 70K, 4K, 20mK as it goes down

#### Trend 2
- 300Kelvin
- uses microstrip

- IBMQ Osprey (with 433 qubits)
    - less complex even with more qubits

#### Trend 3
- hardware in 4 Kelvin
- superconducting wire
    - low wire resistance
    - thinner wires


- Intel Horse Ridge I/ II, Google, IBM

### Challenges: Complex Scalability: Trade-offs
- Temperature choices:
    - 300K CMOS
        - No 4K device power
        - Huge wire power
            - Thick coaxical cables
            - huge heat in the wires
                - limits scalability
    - 4K CMOS
        - Low wire power, fast error decoding
        - Huge 4K device power
            - limits scalability
- Microarchitecture choices
    - every architectural decision has tradeoffs between device power, decoding speed, and error rate

```
Due to the complex scalability trade-offs, it is difficult to build million-qubit quantum computers. -> We need a scalability analysis tool!
```

### Reseach Overview
- Full-stack implementation
- Scalability analysis tool
- 1+M qubit FTQC arch.

### Scalability analysis tool
1. FTQC-Estimator
- predicts frequency and power of each unit for room temperature CMOS and 4K CMOS
2. FTQC-Simulator
- predicts manageable qubit scale and scalability bottlenecks
- uses Cycle-accurate simulation

#### FTQC-Estimator: Validation
- Accurately predicts 4K system power (low error rate)
- well predicts fidelity of current quantum computers
    - compare with 5 IBM quantum computers running 9 quantum applications
    - Build quantum applications (surface code, Hamiltonian simulation, QAOA, VQE...)

### A Million Qubit Scale Quantum Computer System Design
- Build in 3 steps:
- Start from room temperature design
1. Focus on QCI and design 10+K qubit QCI
2. Focus of QCP and design 10+K qubit QCP 
3. Using both, design a million qubit FTQC

#### 10+K qubit QCI: Optimizations
- evaluation while running 3D Jellium application

- 300K QCI
    - Bottleneck: Wire power
    - qubit scale < 650
- 4K QCI
    - Bottleneck: 4K HW power
    - qubit scale < 700

- 3 power reductions
    - no-memory measure
    - lower-bit precision
    - power-efficient ISA
- BUT:
    - Bottleneck: Error 
    - Qubit scale < 20,000

- Error mitigation
    - Faster & accurate multi-round measure
    - Qubit scale: 69,000

``QCI supporting 10+K qubits successful``

#### 10+K qubit QCP: Optimizations
- 300K QCP -> 10K QCP
    - Bottleneck: Slow EDU
    - qubit scale < 250

- Opt #1: Fast EDU
    - Qubit scale < 1700

- New Bottleneck: 300K-4K data transfer

- Guideline #1: Move only TCU & PSU
    - Bottleneck: 4K device power
    - Qubit scale < 970

- Opt #2 &3: Low-power PSU & TCU
    - Qubit scale < 4600

- New bottleneck: slow EDU

- Guideline #2: Move EDU
    - Bottleneck: 4K device power
    - Qubit scale 8100

- Opt #4: Fast & low-power EDU
    - Qubit scale: 59,000

``QCP supporting 10+K qubits successful``

```
Let's increase the qubit scale further! (from 10+K to "Millions")
```

### Overview of designing a million qubit FTQC

#### Multi-DR system overview
- Academia & industry propose a multi-refrigerator (Multi-DR) system
    - qubits at different refrigerators interact with EPR pair generation
- Researchers already demonstrated the remote two-qubit operation
    - ETH Zurich

#### Multi-DR system is the future
- Major industries plan to make the multi-DR system
- Google: 1+M qubit-scale multiple-DR system until 2029
- IBM: multi-DR system in 2026+

#### Challenges in multi-DR systems
1. Erroneous ESM
    - due to use of EPR pair for inter-DR
    - Huge errors
2. Slow & inaccurate error decoding
    - due to errors from million qubits
    - slow sequential decoding
    - setup-dependent results

``Due to huge errors, we cannot run any application even with error correction!``

#### Our multi-DR aware FTQC solutions
- 3 solutions for Low-error ESM sequence
- 2 solutions for fast error decoding
- 1 solution for accurate error decoding

#### Multi-DR Friendly Solutions
- Low-error ESM: Quantum Classic Hybrid ESM
    - uploads quantum computer error to classical computer
        - reduce errors by 3 times
- Fast decoding: Nine-logical-qubit granular decoding
    - EDU search only 9 adjacent logical qubits
    - granular decoding
        - enables parallel decoding without conflict
        - 500 times faster decoding
        - FIRST PARALLEL DECODING IN THE WORLD
- Accurate decoding: Ensemble error decoding
    - setup-sensitive erroneous results
    - Error decoders with different setup
        - select the best EDU with better Decoding result
        - Reduce logical error rate $6.1*10^{10}$ times
#### Evaluation Results
- Three solutions reduce error significantly! 
    - $9*10^{10}$ times less error

``successfully designed a system of million qubit quantum computer!``

## Presentation Summary
- Goal: A million-qubit scale quantum computer system
1. Full-stack FTQC system simulator
2. 10+K qubit system (4K CMOS)
3. Million qubit system (Multi-DR)