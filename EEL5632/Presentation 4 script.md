
---

**(Slide 1: Title)**

Hello, today we will be presenting our critique of the paper, "System safety and ISO 26262 Compliance for automotive lithium-ion batteries".

---

**(Slide 2: Motivations for ISO 26262)**

I'd like to start by covering why this topic matters.

The paper lays out a pretty straightforward motivation: **lithium-ion batteries** are the most common energy storage system in modern **EVs** today. However, they come with **significant hazards** of fire or explosion if thermal runaway were to occur.

This paper points out that while control systems are designed to prevent these dangers, the **control systems themselves** can also fail. A sensor malfunction, a software bug, or a controller failure can be the very thing that causes the dangerous state.

---

**(Slide 3: What is ISO 26262?)**

I'd like to now give a little background on the ISO 26262 standard

So what is it?

It's the international standard for the **functional safety** of electrical and electronic, or E/E, systems in vehicles.

Its purpose is to provide a **framework** to help design, develop, and manufacture these E/E systems safely.

The standard is designed to address hazards from malfunctioning behavior. This includes both **random hardware failures** and **systematic failures**, which includes hardware design flaws or software bugs.

The **goal of this paper** is to apply this standard to the concept phase and system-level development of a hypothetical battery setup, to show how the process works.


---

Slide 4:

First, it's important to clarify the standard's scope. As the paper notes, ISO 26262 does not address physical electrical hazards, like a wire failing on its own.  

Instead, its entire focus is on the electrical control systems that are supposed to protect against those failures.

This is the core workflow for the concept phase, which our presentation will explore further:  

• We'll start with the Item Definition—defining what the system is.

• Then the HARA—the Hazard Analysis and Risk Assessment.

• Then the Functional Safety Concept.

• Followed by the Allocation of Requirements to different parts.

• And finally, the Technical Safety Requirements.

---

**(Slide 15: Critiques)**

Now that we have heard the process of development, I would like to quickly talk about a few critiques we had about this paper.

I'd like to start with the negatives.

First, the scope of the paper felt **narrow**. The paper only focused on the **overcharge protection** aspect and did not touch on the overcurrent or over-temperature aspects, but they do claim that a full paper would need to address these.

Secondly, the battery structure they propose is **overly simplified**. It is only 6 cells, and a modern EV has far, far in excess of this amount. The authors do acknowledge how this would differ in the real world.

On to the positives.

We felt the paper did a great job as an **educational tool**. It provides a clear, step-by-step walkthrough of the concept and development phase, which makes the ISO 26262 standard easier to understand overall.

We also really liked how the paper was **well-referenced**. The authors did a great job highlighting exactly which **clause** of the ISO standard was being applied in each part of the paper.

Thank you all so much, that concludes our presentation. Any questions?