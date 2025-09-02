# Practical Software Diversity
by Professor Koo HyungJoon
- Webpage: https://secai.skku.edu
- Contact: kevin.koo@skku.edu

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

## Compiler-Rewriter Cooperation
- **Reliable**
- **Transparent**
- **Compatible**
- **Cheap**
- compiler and linker knows the metadata information through object files
```
Metadata
- Layout
- Basic Blocks
- Fixups
- Jump Tables
```
1. extract these metadata from compiler
2. update and consolidate the metadata using the linker
3. embed these metadata to the master binary
4. Software vendor can generate the master binary and distribute the master binary executable through legacy distribution channels
5. Users that receive the master binary can generate variants

## Identifying Transformation-assisting Metadata: Layout (1/2)
- main function is the *User-defined Function*
- Find the offset and size of this function

## Identifying Transformation-assisting Metadata: Basic Blocks
- Understand the code using the BBL(Basic Blocks) through assembly and machine instructions

```
If condition
- BBL Offset
- BBL Size
- Fall-through BBL
- Type: BBL
- Type: OBJ
- BBL (bblOff, bblSz, bblType, isFallthru)
```

## Identifying Transformation-assisting Metadata: Fixups and Relocation
- Relationship between fixups and relocations
    - A = {x | x E fixups at compilation time}
    - B = {y | y E relocations in an object fila at linking time, y E A}
    - C = {z | z E relocations in a final executable at runtime, z E B}
    - <u>A **superset** is required for fine-grained randomization</u> 

```
A > B > C
|A| >= |B| >= |C|
```


 - For example, relocations are part of **Set A**, including:
    - Jump tables (for switch-case) *@.rodata*
    - vtables (for C++) *@.rodata*
    - Function pointers *@.data*

## Transformation-assisting Metadata Summary
| Metadata | Collected Information | Collection Time |
| -- | -- | -- |
| Layout | Section offset to the first object | Linking |
| | Section offset to main() if any | Linking |
| | Total code size for randomization | Linking |
| | ``Layout(randOff, randSz, mainOff)`` | |
| *Source type* | *C/C++ Source, Incline-disassembly, or hand-written disassembly (new)* | *Compilation*|
| Basic Block | BBL size (in bytes) | Linking | 
| | BBL boundary type (BBL, FUN, or OBJ) | Compilation |
| | Fall-through or not | Compilation|
| | Section name that BBL belongs to | Compilation |
| | ``BBL(bblOff, bblSz, bblType, is Fallthru)`` | |
| Fixup | Offset from a section base | Linking |
| | Dereference size | Compilation |
| | Absolute or relative | Compilation | 
| | Type (c2c, c2d, d2c, or d2d) | Linking |
| | Section name that fixup belongs to | Compiation |
| | ``Fixup(fixOff, derefSz, fixType, is Absol)`` | |
| Jump Table | Size of each jump table entry | Compilation |
| | Number of jump table entries | Compilation |
| | ``JumpTable(entrySz, numEntries)`` | |

## Metadata Consolidation at Link Time
- Linker consolidates per-object metadata
    - Constructing the final layout
    - Resolving symbols
    - Updating relocation information
    - *(original roles of a linker)*
    - **Merging / adjusting all collected metadata from each object file**
        - Layout: section offset to the first object and the main()
        - BBL size (type: OBJ) update when linker introduces alighnments btn objects
        - Fixup offset adjustment 

## Client-side Randomization
- Static binary instrumentation at installation time
- Rewrite code with master binary

## Serialized Transformation-assisting Metadata

## Putting Everything Together from the Previous Example

## Evaluation for SPEC2006 Benchmark
- 0.28% runtime overhead on avg. and 11.46% increase in file size

## Wrap-Up
- Compiler-assisted Code Randomization
    - Function and basic block level permutation
    - Facilitated by transformation-assisting metadata stored within augmented executables
    - Transparency, reliability, and compatibility
- Open-source prototype:
    https://github.com/kevinkoo001/CCR