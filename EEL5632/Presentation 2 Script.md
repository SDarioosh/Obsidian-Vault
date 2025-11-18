### **(Slide 16: Multi-Sensor Consistency Check)**

_(Start of speech)_

"Hello everyone. So far, we've discussed attacks that can fool a single sensor and a defense called PSA that makes an individual sensor more robust. Now, I'd like to talk about the second defense strategy: the **Multi-Sensor Consistency Check**, or MSCC. This is a clever way we can use an entire array of sensors to not only determine the true location of objects but also protect against attackers trying to spoof them.

The core idea of MSCC is to move away from relying on one sensor and instead use multiple sensors to cross-verify each other's data and confirm an obstacle's location.

Here’s how it works: a single sensor sends out a ping, but at least three sensors—including the original one—listen for the return echo. The measurement from the transmitting sensor gives us a distance based on the Time-of-Flight, which we can map as a **circle** of possible locations.

Next, the system looks at the difference in the echo's arrival times at the two other listening sensors. This time difference creates a **hyperbola**. As we can see in the diagram, the true location of the object is the single point where that circle and hyperbola intersect.

So, that's the basic geometry. **Now, let's look at how this same principle allows us to detect an attack.**"

---

### **(Slide 17: Detecting Attacks)**

"An echo that reflects off a real object will always produce a single, consistent point of intersection, just like we saw in the last slide. However, a spoofed signal is a lie. The attacker is transmitting from a different location than the supposed object, and this creates a fundamental conflict in the geometry.

When the system tries to triangulate this fake signal, the intersections don't match up, resulting in an inconsistent location. The system immediately detects this inconsistency and rejects the data. As you can see in the diagram, the fake signal, shown in **red**, causes the lines that are supposed to converge to create **two separate points** of intersection instead. This tells the system that the signal is not legitimate and should be rejected.

This system has another powerful ability: since we are triangulating the fake signal instead of the spoofed object, we can actually pinpoint the location of the **attacker's device** itself."

**"To make this defense even more robust, the researchers proposed an 'Enhanced MSCC' layout.**"

---

### **(Slide 18: Enhanced MSCC)**

"This enhanced version uses two dedicated 'listening-only' sensors right next to each primary sensor, creating a **'sensor triplet'**. The main advantage is that this setup enlarges the overlapping detection area, which makes it much more likely that multiple sensors can 'hear' the same echo, boosting the system's triangulation ability.

The authors tested this concept in MATLAB, and the results are clear from the figure. The '4 triples' configuration—which is 12 sensors in total—dramatically improves the detection rate, especially at close range. It even outperformed a system with 12 sensors simply arranged in a straight line. The second graph also shows that the detection rate gets better as the sensor's beam angle gets wider."

**_(Clear Break for Next Slide)_**

**"Although MSCC sounds very promising, it's important to consider some of the critiques I had after reviewing the paper.**"

---

### **(Slide 19: Critique of MSCC)**

"First, the effectiveness of MSCC was **only tested in MATLAB** and had no real-world testing. Seeing how this algorithm performed on actual moving vehicles would have been a much stronger validation of the concept.

Secondly, the simulation did not account for any **moving objects**, like another vehicle or a pedestrian. This is a critical factor that would need to be handled before it could ever be implemented in the real world.

Finally, there is the practical issue of cost. The **Enhanced MSCC requires the manufacturer to triple the number of sensors** on the vehicle. This would significantly increase the financial cost and the computational load on the car's systems.

This concludes my analysis of the MSCC system. Thank you."