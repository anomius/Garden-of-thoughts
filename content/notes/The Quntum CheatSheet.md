---
title: "The Quntum CheatSheet"
tags:
- "Quantum Computing"
- "Physics"
- "Knowlege"
---
## Introduction

---

**Disclaimer** The aim of this cheatsheet is to provide you with a quick resource to check and come back on the main intuitions around the famous textbook algorithms. This is not aimed at providing a full blown detailed explanation of each algorithm. The guide assumes you have understood the algorithms in detail already.

This cheatsheet includes a quick and handy summary of the intuitions behind each of the well known textbook quantum algorithms. We cover the followin algrithms:

-   [**Deutsch-Jozsa**](notes/The%20Quntum%20CheatSheet.md#Deutsch-Jozsa): Finding wwhether a blackbox function is constant or balanced
-   [**Bernstein- Vazirani**](notes/The%20Quntum%20CheatSheet.md#Bernstein-Vazirani): Finding the constant used in a blackbox function
-   [**Simon**](notes/The%20Quntum%20CheatSheet.md#Simon): Finding the period of a function that maps pairs of inputs tot he same output
-   [**Teleportation**](notes/The%20Quntum%20CheatSheet.md#Teleportation): Copy one state from Alice to Bob
-   [**Superdense Coding**](notes/The%20Quntum%20CheatSheet.md#Superdense%20Coding): Encode 2 pieces of data within a qubit
-   [**Grover**](notes/The%20Quntum%20CheatSheet.md#Grover): A search algrithm
-   [**Quantum Fourier Transform**](notes/The%20Quntum%20CheatSheet.md#Quantum%20Fourier%20Transform): Encode / Decode wave signal data
-   [**Quantum Phase Estimation**](notes/The%20Quntum%20CheatSheet.md#Quantum%20Phase%20Estimation): Guess the global phase added by a given quantum operation
-  [**Shor's Period Finding**](notes/The%20Quntum%20CheatSheet.md#Shor's%20Pheriod%20Finding): Find the period of the modular exponentiation function core to Shor's algorithm

Most of these algorithms rely on two core techniques that we'll sumamrize here. The cheatsheet is accompanied by some more in depth jupyter notebooks in the notebooks folder where you'll find more elaborated and in-depth explanations of the algorithms always putting intuition and simplicity at the forefront.

### Technique #1: Phase Kickback

**Goal**: One of the main goals and typical usages of this technique is to read out hidden structural information about a quantum operation

**General Concept**: For every quantum operation there exist a unique set of states to which the operation will not have any effect other than adding a global phase to the state. These states are called the eigenstates of that operation. If we control a given operation with a qubit in equal superposition, this global phase will be kicked back as relative phase for the control qubit if the target qubit is in one of these "eigenstates"

**Usage Example**: A common set-up involves setting your input qubits in the + state and one (usually the one to be used as output) qubit in the - state. After executing the given blackbox function we apply Hadamard gates to our input qubits again in order to discover whether the blackbox is using CX gates. The - state is an eigenstate of the X Gate.

**Algorithms**: These technique is used in the following algorithms

-   Deutsch-Jozsa
-   Bernstein- Vazirani
-   Quantum Phase Estimation

### Technique #2: Partial Measurement

**Goal**: The goal fo this technique is to filter down / get rid of unnecessary parts of a quantum state

**General Concept**: Given 2 entangled registers, if we measurene of them, we will at the same time change the state of the other one revealing an instance of the correlations between the previously entangled registers.

**Usage Example**: in order to find if multiple inputs of a function give the same output we can input an equal superposition to the function and then only measure the output register. because the function will necessarly entangle the input and output registers, when we measure the output register, our input register will also change to include a superposition of only those input values that lead to the measured output.

**Algorithms**: These technique is used in the following algorithms

-   Simon
-   Teleportation
-   Superdense Coding
-   Shor's Period Finding

---

## Deutsch-Jozsa

---

### Goal

Find if a blackbox function with binary output (0 or 1) is constant or balanced

### General Strategy

We use phase kickback in order to determine whether the blackbox function is using CX gates. Because we know the function has binary output, we know the function will be using X gates (or any bit flip equivalents). If the function is constant, these gates will not be controlled by the input and therefore no phase kickback will be detected. On the other hand, if the function is balanced we know that the blackbox will be using CX gates in order to set the output register as a function fot he input qubits. This CX gates will then triger a phase kickback and we will be able to detect it by reading the input qubits after a layer of Hadamard gates.

### Steps

-   Step 1: Put input registers into equal superposition
-   Step 2: Put output qubit tot he - state (eigenstate of the X gate)
-   Step 3: Run the blackbox against the registers prepared in Step 1 & 2
-   Step 4: Apply a layer of Hadamards to the input qubits and measure
-   Result: If we measure any of the qubits to be 1, it means the blackbox is balanced

---

## Bernstein-Vazirani

---

### Goal

We are given a blackbox function that we know it's multiplying bitwise our binary input by a constant s module 2. This means the output of the function is als binary (0 or 1) but i's a function of this constant times our input. We are asked to find the constant.

### General Strategy

We will use phase kickback in order to see which qubits are used to control the output

### Steps

-   Step 1: Put input registers into equal superposition
-   Step 2: Put output qubit tot he - state (eigenstate of the X gate)
-   Step 3: Run the blackbox against the registers prepared in Step 1 & 2
-   Step 4: Apply a layer of Hadamards to the input qubits and measure
-   Result: The bitstring we measure is actually the constant we are looking for. This is because we know the blackbox is doing bitwise multiplication and therefore the constant must be encoded by using controls for each bit that's set to 1

---

## Simon

---

### Goal

We are given function that we know maps exactly 2 inputs to the same output across all its domain (possible inputs) and the difference between each pair of inputs is the same for all pairs of inputs. For example a function that maps:

-   1, 4 -> 1
-   2, 5 -> 2
-   3, 6 -> 3
-   etc.

Find the difference (for the above example 3

### General Strategy

We will feed the function with a superposition of values so that it computes the output in superposition as well entagling the input and output registers. We can then ideally performe a partial measurement on the outcome which will collapse our input to one particular superposition of inputs like (1+4, or 2+5 from the example above). With some additional measurements we can then recover the values and calculate the difference classically.

The partial measurement technique is not always implementable in hardware so you can also just do measurements of all the qubits and then do post selection (select the subset with equal output) in order to recover the desired input.

### Steps

-   Step 1: Put input registers into equal superposition
-   Step 2: Run the blackbox
-   Step 3: Measure (here you need a decent number of shots)
-   Step 4: post select and calculate result classically

---

## Teleportation

---

### Goal

Given an unknown 1 qubit state in 1 QPU, recreate it in another QPU

### General Strategy

Entangle your state with one of the qubits in an already entangled pair and apply a Hadamard gate to it (to your src state). You can think of this intuitively embedding all possible combinations of amplitudes and phases into the entangled pair We will then send the other qubit to the target QPU and use the partial measurement technique on the source QPU so that the target QPU register collapses into one of the encoded possibilities. The results of your partial emasurement will dictate what type of corrections need to be performed on the target QPU in order to recreate the initial state.

-   Note #1: Your src state has now been lost. You can't copy states in a QPU
-   Note #2: In order to apply the corrections to the target QPU, this info needs to be sent via classical channels to wherever the QPU is located so no faster-than-light communication possible

### Steps

-   Step 1: Get / Prepare an entangled pair (Bell state 00+11)
-   Step 2: Entangle the src state with one of the qubits and send the other one to the target QPU
-   Step 3: Apply a Hadamard gate to the src state and measure both the src state and the half of the bell pair that stayed in the src QPU
-   Step 4: Based off of the measurement results apply corrections (X or Z gates) to the target QPU

---

## Superdense Coding

---

### Goal

Given 2 classical bits of information encode them into 1 qubit and send them over to another QPU

### General Strategy

**Encoding**: We need an encoding strategy than can reliably be decoded as well in order to recover the 2 bits of information. The general strategy will be to encode the classical bits in a previously entagled pair: one bit by using the amplitudes of the pair (so either using the standard bell pair 00+11 or transforming it to the 01+10 version of it) and another one by using the relative phase of the entangled state. This can be done by using a conditional X and a conditional Z gates respectively.

**Sending**: The half of the bell pair frrom he src QPU needs to eb sent to the target QPU for decoding

**Decoding**: In order to read the classical bits back we simply need to apply a CX gate so that we deterministically turn one half of the pair to measure always 0 or 1 and then apply a Hadamard gate to the other one so that we can capture whether the phase was + or - and determine the ther classical bit of information

**Note**: This does also not imply faster-than-light communication because the target QPU needs to have the entire bell pair in order to decode the data. This means the src QPU entangled half needs to be sent over to the target QPU destination.

### Steps

-   Step 1: Get / Prepare an entangled pair (Bell state 00+11)
-   Step 2: Encode one bit by applying an X gate conditined by the classical bit and the other one using a Z gate also conditined by the classical bit
-   Step 3: Send the half pair from src to target QPU
-   Step 4: Apply a CX from src to target half, apply a Hadamard gate to the src half and then measure to recover the classical bits

---

## Grover

---

### Goal

Coming Soon...

### General Strategy

Coming Soon...

### Steps

Coming Soon...

---

## Quantum Fourier Transform

---

### Goal

The goal of this algorithm is to take [frequency domain](https://en.wikipedia.org/wiki/Frequency_domain) input and generate the corresponding [time domain](https://en.wikipedia.org/wiki/Time_domain) data. In other words, it will interpret the input as a frequency or set of frequencies (if a superposition is given) and it will generate time-based data using our computational base elements as discrete time steps. the encoding is done by using he relative phases of each computational base element. The data is encoded using counter-clockwise rotations

**invQFT**: The inverse of these operation is the same but the rotations are done clockwise.

**Superposition**: Coming Soon...

### General Strategy

The general strategy will be to use the binary representation of our input to pick the right amount of rotation that needs to be selectively applied. As an example let's imagine our register has 4 qubits. Whether the lowest bit is a 0 or a 1 dictates the amount of rotation that needs to be applied to the |1000> computational element. The rotations will be achieved with a combination of Hadamard and controlled rotation gates. The use of Hadamards is important because it will also guarantee that we build an equal superposition while adding a phase rotation component as well.

### Steps

Coming Soon...

---

## Quantum Phase Estimation

---

### Goal

The goal is to find the phase that a known operation applies to one of it's given eigenstates

### General Strategy

The general strategy will be to use phase kickback in order to register the global phase applied to a work qubit and encode it as a phase gradient in our superposed i/o register so that we can then decode it with the invQFT.

We will setup an input register x in superposition and then apply the operation U**x (or simply operation U, x times) to a pre-initialized work qubit with the given eigenstate. because the work qubit is in an eigenstate of U, the registers will not get entangled, instead each element of the superposition will get a kickedback relative phase proportional to it's own value (i.e. the element 3 will get U's phase 3 times kicked backed).

The invQFT will tell us with what frequency our final relative phases are rotationg across our register with precision 2**n (n = number of qubits). If we divide the frequency by the precision of our register we basically uncover how much phase (proportionally speaking) one single run of U adds to yur work qubit

### Non-eigenstates

Coming soon...

### Steps

-   Step 1: Prepare exponent register in superoposition (egister x)
-   Step 2: Prepare a work qubit in the given eigenstate of U
-   Step 3: Apply U**x
-   Step 4: Apply the invQFT to register x

---

## Shor's Period Finding

---

### Goal

The goal is to find the period of a the **B**A mod R** function.

### General Strategy

The general strategy will be to prepare a register in superposition in order to use it as exponent for the **B**A mod R** function and therefore "parallelize" the calculations. We will then use the fact that the registers get entangled in a way such that for each repeated result, we build up a superposition of the exponents that lead to it. These exponents are by definition equally spaced and if we treat each of this exponents as inputs in the [frequency domain](https://en.wikipedia.org/wiki/Frequency_domain) and apply the QFT to them (in superposition), the superposed [time domain](https://en.wikipedia.org/wiki/Time_domain#:~:text=Time%20domain%20refers%20to%20the,data%2C%20with%20respect%20to%20time.) outputs will reveal the spacing from which we can classicaly try and pick up the desires result.

### Steps

-   Step 1: Prepare exponent register in superoposition
-   Step 2: Prepare the output register with a non zero value so that **B**A mod R** can actually work
-   Step 3: Apply **B**A mod R**
-   Step 4: Apply QFT to the exponents register
-   -   This works because superposing the resulting waves will lead to a resulting interference pattern with a "beat" frequency equal to what we are looking for
-   Step 5: Read out and post-process the potential solutions
-   -   Note that when reading frrom the register we will read one of the frequency peaks so we still have to do trial and error until we can guess the actual frerquency