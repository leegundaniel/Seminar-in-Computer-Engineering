# Practical Software Diversity
by Professor Koo HyungJoon

## Moving Target Defense (MTD)
A new defense paradigm since 2009
- From a passive to an active defense against cyber attacks
- Periodically / non-periodically change a target
- Increase the cost(complexity) for a successful attack

``
When a gun shoots a target, the MTD concept is moving the target away from the gun's trajectory
``

Examples:
- Network
    - Dynamic IP / Port
    - Routing path alteration
    - Proxy location randomization
- Host (Operating system, application)
    - Dynamic runtime environment(e.g., memory layout; ASLR)
    - OS type, version alteration
    - Code / data randomization

## Code Injection Attacks
An attacker injects a carefully crafted exploit via a buffer


1. Exploit the payload caused by the local variable buffer in a stack (``stack overflow``)
2. Overwrite the initial code using the attacker's injected code

### Injection Becomes Non-negligible
Canary
- random number inserted in the stack
- used as an inspection tool for injections
- if the canary value has been corrupted or overwritten
    - the code has been attacked or modified

NX (No-Execute) / DEP (Data Execution Prevention)
- If the NX Memory has been taken or modified, the attacker will be unable to execute the injected code
- Considered a writable XOR executable policy
    - Writable memory cannot be executed, vice versa

## Code Reuse Attacks
An attacker can leverage the existing code
- If attacker knows the exact location of a code, one could collect all code snippets (machine instructions) beforehand

## Current Mitigation: ASLR
Address Space Layout Randomization
- Randomizing the base addresses of segments at load time
- Breaking attacker's assumption of knowledge of code layout in memory
- Introducing artificial diversity weakens address space predictability
- Not sufficient as the intra-layout inside the code stays intact (e.g., information leak)
    - Relative code data is identical
    - If a single code pointer is leaked, the other codes can be calculated

## Better Defense: Diversify Code Itself
**Compiler-assisted Code Randomization**

### Motivation
- Non-executable memory an ASLR have been the *only* widespread deployed mitigations
- Many software diversification techniques have been proposed
- However, they have mostly remained an <u>academic exercise</u>

## Key Factors for Practical Deployment of Code Randomization
- Existing proposals fall into two main deployment models

|           | By *end users* | By *software Vendors* |
|-----------|--------------|---------------------|
| How | - Source code recompilation | -Variant generation |
| | - Binary instrumentation | - Delivery to each user |
| Downsides | -Source code availability | - High computation |
| | - A complex analysis | - Network distribution (caching / CDNs) |
| | - Unreliable mutations | |

- In general, (accurate) static binary analysis is challenging
    - Identifying indirect calls / jumps in a CFG/CG is undecidable
    - Distinguishing code from data in undecidable

# 25분 30초
Compiler-Rewriter Cooperation