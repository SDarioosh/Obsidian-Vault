
**(Slide 10: Application Modules > Overview)**

"Good afternoon, My name is Shahyah and I’ll be presenting the application modules section. Now that we've covered how the SAFELANE system perceives the world, let's dive into the brains of the operation: the **Decision Layer** and its **Application Modules**

The decision system's primary role is to analyze the current driving situation, identify any risks, and then suggest the proper action for the lane-keeping function to perform . To achieve this, it relies on critical data from several key modules. We will now go through each of these components, starting with how the system plans for the road ahead."

---

**(Slide 11: Application Modules > Most Likely Path)

"The first key module is the **Most Likely Path**, or **MLP**. While the vehicle's onboard sensors have a limited physical range, the MLP module looks much farther down the road. It predicts the most probable route by using data from digital maps, the car's current speed and acceleration, and an 

**Electronic Horizon** sensor.

This 'Electronic Horizon' acts as a virtual sensor, providing information retrieved from a digital map database, which effectively extends the system's foresight far beyond what physical sensors can see. The MLP can deliver this path either for a fixed distance ahead, like 900 meters, or for a defined time, like the next 10 seconds ."

---

**(Slide 12: Trajectory Estimation Modules)**

"Next, we have the **Trajectory Estimation Module**, or **TEM**. Where the MLP provides a long-term route, the TEM focuses on the immediate future, aiming to predict the driver's short-term intentions. Essentially: what is the driver expected to do in the next few seconds? 

The TEM has two main sub-functions. The first is 

**Dynamic Trajectory Estimation**, which determines the likely path based on the vehicle's current movement and properties .

The second is 

**Lane Change Prediction**, which compares that predicted trajectory to the geometry of the lane . This module is also critical when lane markings aren't visible, as it can act as a dead-reckoning function to assist the Lane Data Fusion module in the event the vehicle can not see lane markings."

---

**(Slide 13: Dynamic Trajectory Estimation)**

"Diving a bit deeper, 

**Dynamic Trajectory Estimation** is used to predict whether the vehicle will change lanes soon, but it does so without using the road's geometry . Instead, it relies on vehicle dynamics models like the 

**Constant Turn Rate** and **Constant Tangential Acceleration** models, which consider the car's yaw rate and acceleration .

To ensure accuracy, the system uses a 

**Kalman Filter** to reduce measurement noise from the sensors. it uses vectors to calculate the position of the vehicle over time, and the final output is a matrix representing the vehicle's predicted location over time, giving the system a picture of the car's immediate future path."

---

**(Slide 14: Lane Change Prediction)**

"The  **Lane Change Prediction** function takes the trajectory we just calculated and compares it to the current lane geometry. This allows it to compute the 

**Time to Lane Crossing**, or **TLC**, which is the time available before the vehicle crosses a lane boundary.

A **slow decrease** in TLC often indicates a drowsy driver, while a **fast decrease** can signal a loss of control . However, calculating TLC in real-time is computationally costly and difficult with sensor limitations . Because of this, the system uses two different approaches to handle it."

---

**(Slide 15: Lane Change Prediction Approaches)**

"The two methods are the **Static Approach** and the **Dynamic Approach**. The Static approach is simpler; it uses the vehicle's current lateral velocity and acceleration and assumes the road ahead is straight .

The **Dynamic Approach** is more advanced. It directly compares the vehicle's projected trajectory to the lane's geometry. The intersection of these two paths determines the Time to Lane Crossing. This method also calculates more robust metrics like the 

**Lane Predicted Minimum Distance**, or **LPMD**. Instead of just waiting for a lane crossing, the system calculates the closest point the vehicle will get to the lane boundary in the near future. The second metric is the **Time to Lane Predicted Minimum Distance**, or **TLPMD**, which is simply the time it will take to reach that closest point which once reached will trigger a warning.

As you can see from the performance trial graphs, the dynamic approach leads to earlier prediction, 3.6 s before lane departure against 2.4 and 1.9 s, 

and generates fewer false alarms in lane-drifting scenarios, making it far more reliable."

---

**(Slide 16: Situation Model)** 

"All of this data—the Most Likely Path, the fused lane data, and the future trajectory—feeds into 

the  **Situation Model**. This module's job is to build a comprehensive model of the current driving situation using all available data.

It works by selecting the most likely predefined scenario based on everything it knows: the properties of the lane, the vehicle's status, and the driver's estimated maneuver. This is what makes the SAFELANE system 'situation-adaptive'

---

**(Slide 17: Self-Assessment)** 

"Of course, making a decision is only useful if the system is confident in its data. This is the responsibility of the **Self-Assessment** module.

This component continuously estimates the confidence and reliability of the system's own output. This is a critical safety feature. If the system's reliability is determined to be 

**high**, it can authorize an active steering correction. However, if the reliability is 

**low**, it will only issue a warning to the driver instead of taking direct control."

---

**(Slide 18: Decision Model)** 

"Finally, we arrive at the **Decision Model**. This module takes all the inputs—the scenarios from the Situation Model, and the TLC and LPMD values—and decides what action needs to be taken based on the current risk of a lane departure .

It uses a fuzzy-like controller as the data will rarely be black or white to determine if a predicted lane departure is intentional, like a planned lane change, or unintentional, like drifting. Based on this, it determines the final action, converts it into the proper format, and sends the command to 

the **Actuator System**, which then provides the warning be it sound or a haptic vibration motor or steering input.

This concludes the look at the application modules, and now I would like to hand it over to Johnathan to tell you more about the Actuator system.