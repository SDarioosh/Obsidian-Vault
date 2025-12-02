# Slide 1
---

Hello, we are **Team Lightning McQueen**, and today we will be presenting our final project on our **Smart Lane-Changing System**.

# Slide 2
---

As we move towards a **future dominated by autonomous vehicles**, the way vehicles interact on the road will **fundamentally change**. Instead of relying on **visual cues**, the vehicles will be able to **directly communicate** with each other.

This can **alleviate congestion**, as it will allow for much **quicker actions** without misunderstandings or emotions getting in the way. An important **downside**, however, is the **susceptibility to attacks** from bad actors.

# Slide 3
---

I'd like to quickly discuss how we **developed this project**. We used **SUMO**, which is a traffic simulator, and we leveraged the **TraCI library** to allow us to control SUMO using **Python**.

The **roadway** we used for testing is a **5-lane highway** that does not contain **on- or off-ramps**, as our algorithm solely focuses on **negotiation** between vehicles.

# Slide 4
---

Our algorithm has **3 levels of complexity**.

The **first level** is the **simplest**, as it only checks the vehicles **in front and behind** the ego vehicle to ensure they won't also change lanes, possibly causing a **collision**.

**Level 2** expands upon this and checks possible **conflicting vehicles** in the **target lane** as well, to ensure no **collisions**occur.

**Level 3** is the **most complex**; in addition to checking everything in Levels 1 and 2, it also checks the **lane adjacent to the target lane**. This ensures that no vehicles from that lane want to enter the **target lane** at the same time as the **ego vehicle**.

We send the **requests** to change lanes in the form of a **packet** that contains information about the vehicle sending it, such as **speed**, **acceleration values**, and more.