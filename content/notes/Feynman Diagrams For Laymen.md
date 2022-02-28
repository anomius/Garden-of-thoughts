---
title: "Feynman Diagrams For Laymen"
tags:
- "Physics"
- "Knowlege"
- "Quantum"
---
# Feynman Diagrams For Laymen

## Introducing the most important doodles in Quantum Mechanics

Richard Feynman is one of the coolest physicists to ever exist. He’s had several contributions to the science, and scientific community particularly to the science of quantum mechanics. The physicist shared the 1965 Nobel Physics Prize for his works on Quantum Electrodynamics with Julian Schwinger and Sin-Itiro Tomonaga. One of such notable contributions of Richard Feynman are the _Feynman diagrams,_ the simple yet elegant “_doodles”_ in quantum mechanics which describe the fundamentals of particle interactions which otherwise would be quite complex to understand, at least for a non-physics major_._ But what are these diagrams and what do they represent? How are they related to quantum physics? In this article, I shall try to simplify and explain the most important diagrammatic representation in all of physics.

![](https://miro.medium.com/max/700/1*j1i4NKSIoLqkgN5GE3l43Q.jpeg)

Richard Feynman at Caltech. Caltech Archives Image.

## Where did it all start?

It was in 1948, at the Pocono Conference where Richard Feynman first introduced these diagrams. In the spring of 1949, he published a paper explaining the Feynman diagrams. These kinds of pictorial or diagrammatic representations weren’t really new at the time. [Ernst Stueckelberg](https://en.wikipedia.org/wiki/Ernst_Stueckelberg), a Swiss student at the time, had developed a diagrammatic approach of representing elementary particle interactions and published during somewhere between 1943–45. But it was Richard Feynman who sort of refined and brought the visual representations to fruition.

Now, these diagrams are extremely useful for theorists and made the calculations much easier by presenting complicated mathematical equations as _trajectories._ This was the reason, why Niels Bohr (who, by the way, was an attendee at the Pocono Conference) got furious and reportedly stated that Feynman didn’t _know_ quantum mechanics.

## Why do particles interact?

Interactions happen everywhere. I mean particle interactions. They are the reason behind the existence of massive stars and galaxies. The chemical reactions take place as a result of these interactions. Pretty much anything exists due to particle interactions. In elementary particle physics, there are two very important types of particles namely fermions and bosons. Fermions are matter particles (for example, electrons) whereas Bosons are force carriers (for example, photons). These fermions interact at the most fundamental level by emission or absorption of force carriers. In case of electromagnetic interaction, they emit or absorb photons. And for different other fundamental forces, their corresponding force carriers are absorbed and emitted. This is where Feynman diagrams come into place. These two-dimensional figures exhibit the interaction of fermions and bosons in the most simple and elegant manner. Let’s try and understand these diagrams step-by-step.

## What are Feynman diagrams?

![](https://miro.medium.com/max/700/1*uGz8OcGiEov87fU_8X9OrA.jpeg)

A simple Feynman diagrams with space-time axes. Image © Romainbehar, CC0, via Wikimedia Commons

In the above diagram, the straight trajectories are representing the matter particle (in this case electrons) and the wiggly line is representing the force carrier (in this case photons). The space and time parameters don’t really have to be placed in the exact same axes as shown in the diagram above. Thus, this diagram shows the ordinary force of repulsion between two electrons. The photons emitted are called _ghost particles_ or _virtual particles_ as they come into existence for an extremely small amount of time- so small that it can temporarily violate the conservation of energy. Sometimes the continual possibility of the photons coming into existence and vanishing causes increasing complexity. The point at which the three lines (in rare cases four lines) is known as a vertex and it has its own symbolic representation in terms of mathematical equation depicting the same interaction which I shall explain later in the story.

![](https://miro.medium.com/max/700/1*AbwgtVj-i9I2fUQOxeGnMw.png)

The Feynman diagram representation of electromagnetic interaction along with the corresponding parts of Feynman Integral. Image credit: [Fermilab](https://youtu.be/hk1cOffTgdk)

The Feynman diagrams aren’t just for ordinary particles. In fact, they also represent antiparticles for which the direction of the arrowhead is reversed showing antiparticles as normal particles moving backward in time.

There can be many Feynman diagrams for one simple interaction with countless possibilities. Drawing all possible diagrams shows how quickly the permutations grow. Higher the permutations, more complex the calculations become. However, when the complication with the diagram increases, the probability of the interactions become lesser. Each diagram corresponds to a mathematical expression, as stated earlier, which calculates the probability. The mathematical calculations are complex for someone with a non-physics background of course.

![](https://miro.medium.com/max/539/1*Bq80kBUc10GLF_a_KD7IgQ.jpeg)

Different possible Feynman diagrams for the electron interaction and exchange of photons.

Diagram (a) and (b) show the interaction of electrons where one of the electron emits a second photon that is absorbed by the other electron. Diagram (d) shows the movement of photon from one electron to the other and in doing so it temporarily forms an electron-positron pair (depicted by the circular path in the diagram). Diagrams (e) and (f) depict the interaction of electrons where one of electrons emit an additional photon that is absorbed by another either before or after the big scatter. Diagrams (g), (h), (i) and (j) show the electromagnetic interaction where a virtual photon is emitted and reabsorbed by one of the electrons either before or after the main interaction.

Feynman diagrams come in handy while representing the interactions of matter in doing the quantum mechanical calculations. Unfortunately, in order for you to do those complex calculations you must take quantum mechanics, quantum field theory to be more specific, in your grad classes. 

_References:_

[https://www.askamathematician.com/2010/10/q-what-are-feynman-diagrams-how-are-they-used-theoreticallypractically-and-are-there-alternativecompeting-diagrams-to-feynmans/](https://www.askamathematician.com/2010/10/q-what-are-feynman-diagrams-how-are-they-used-theoreticallypractically-and-are-there-alternativecompeting-diagrams-to-feynmans/)  
[https://www.sciencedirect.com/topics/chemistry/feynman-diagram](https://www.sciencedirect.com/topics/chemistry/feynman-diagram)  
[https://www.secretsofuniverse.in/feynman-diagrams/](https://www.secretsofuniverse.in/feynman-diagrams/)

[_Gleick, James, and Freeman J. Dyson. Genius: The life and science of richard feynman. CNIB, 2012._](https://webmail.psych.purdue.edu/9bir1c88eeyu/07-jettie-hahn/g-9780679747048-genius-the-life-and-science-of-richard-feynman-p.pdf)

# Simon

---

#### Goal

We are given function that we know maps exactly 2 inputs to the same output across all its domain (possible inputs) and the difference between each pair of inputs is the same for all pairs of inputs. For example a function that maps:

-   1, 4 -> 1
-   2, 5 -> 2
-   3, 6 -> 3
-   etc.

Find the difference (for the above example 3

#### General Strategy

We will feed the function with a superposition of values so that it computes the output in superposition as well entagling the input and output registers. We can then ideally performe a partial measurement on the outcome which will collapse our input to one particular superposition of inputs like (1+4, or 2+5 from the example above). With some additional measurements we can then recover the values and calculate the difference classically.

The partial measurement technique is not always implementable in hardware so you can also just do measurements of all the qubits and then do post selection (select the subset with equal output) in order to recover the desired input.

#### Steps

-   Step 1: Put input registers into equal superposition
-   Step 2: Run the blackbox
-   Step 3: Measure (here you need a decent number of shots)
-   Step 4: post select and calculate result classically

---