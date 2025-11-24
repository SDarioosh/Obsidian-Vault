
Here is a complete 8-minute presentation script based on your provided files and instructions, tailored for your two-person team.

This script is structured to follow your contributions as listed in your reports (Sean: 1, 3, 4A; Shahyah: 2, 4B, 5) and places the required focus on Algorithms 2, 4, and 5.

---

### 🎬 Video Presentation Script (8 Minutes)

**Speakers:**

- **Sean:** Member 1
    
- **Shahyah:** Member 2
    

---

#### Section 1: Introduction & Contributions (1 minute)

**(Speaker: Sean)**

> "Hello everyone, I'm Sean."

**(Speaker: Shahyah)**

> "And I'm Shahyah. This is our final project presentation for 'Maximum Value Vault Selection.' "

**(Speaker: Sean)**

> "Our project's goal was to solve a problem: given `n` vaults, each with a specific value, we needed to find the subset of vaults that gives the maximum total value. The main constraint is that no two chosen vaults can be within `k` positions of each other.
> 
> We designed, implemented, and tested five different algorithms, from simple greedy heuristics to fully optimized dynamic programming solutions."

**(Speaker: Shahyah)**

> "As for our team's contributions: * **Sean** focused on Algorithm 1, the brute-force recursive Algorithm 3, and the top-down memoized version, 4A. * **I** (Shahyah) focused on the two-pointer greedy Algorithm 2, the bottom-up Algorithm 4B, and the optimized linear-time Algorithm 5. 
> 
> Today, we'll walk through our findings for all five, with a special focus on Algorithms 2, 4, and 5."

---

#### Section 2: The Heuristics & Brute Force (Algorithms 1, 2, 3) (2.5 minutes)

**(Speaker: Sean)**

> "First, we'll briefly cover our baseline algorithms.
> 
> **Algorithm 1** was a simple, right-to-left greedy approach. It assumes the best vault is at the end, so it starts at index `n-1`, 'takes' that vault, and then jumps `k+1` steps to the left, repeating this process. It's linear, O(n), but as it shows in our report 'Plot 9', it's **not optimal** for the general problem. 
> 
> To find a _correct_ answer, we implemented **Algorithm 3**, which is a brute-force recursive solution. As you can see in `program3.py`, the `solve(i)` function recursively explores two choices for every vault: 1.  **Skip** the vault and solve for `i+1`, or 2.  **Take** the vault, add its value, and jump to solve for `i+k+1`. 
> 
> While this is correct, it has an **exponential runtime of O(2n)** because it recalculates the same subproblems over and over. You can see in our report's 'Plot 3' that it's unusable for even small inputs. "

**(Speaker: Shahyah)**

> "That brings us to **Algorithm 2**, which was our second greedy attempt. This one required more focus.
> 
> * **Design:** I implemented a **two-pointer greedy approach**, which you can see in `program2.py`. One pointer starts at the `left` (index 0) and the other at the `right` (index `n-1`). 
> 
> - **Logic:** In each step of the `while` loop, it compares `values[left]` and `values[right]`. It 'takes' the vault with the **larger value**, adds it to the total, and moves that specific pointer inward by `k+1` steps. 
>     
> - **Analysis (Analysis 2):** Like Algorithm 1, Since the pointers only move towards the center, it's a linear **O(n)** algorithm. 
>     
> - **Correctness:** However, despite being a 'smarter' heuristic, it is **still not optimal**. A greedy choice at one end can prevent a better combination of vaults later.
>     
> 
> So, both of our O(n) greedy algorithms were fast but incorrect. And our one correct algorithm was exponentially slow. To get both speed and correctness, we had to use dynamic programming."

---

#### Section 3: Dynamic Programming (Algorithms 4 vs. 5) (3 minutes)

**(Speaker: Sean)**

> "To fix the exponential runtime of Algorithm 3, we developed **Algorithm 4**, which uses dynamic programming to store and reuse subproblem results. 
> 
> I implemented the top-down version, **4A**, which is just the recursive Algorithm 3 but with a `memo`dictionary to store results. As you can see in `program4A.py`, this required us to increase Python's recursion limit just to run."

**(Speaker: Shahyah)**

> "And I implemented the bottom-up version, **4B**. This algorithm fills a DP table iteratively, `var1`, using the same core recurrence: the max value at any vault `i` is the maximum of _skipping_ it (getting the value from `i+1`) or _selecting_ it (getting `values[i]` plus the value from `i+k+1`). 
> 
> Both 4A and 4B find the correct, optimal answer. **But they are not linear.** This brings us to the most important contrast of our project.

**(Speaker: Shahyah)**

> "Let's contrast **Algorithm 4 vs. Algorithm 5**. Both are correct DP solutions, but they have different time complexities because of _how they reconstruct the path_.
> 
> - **In Algorithm 4 (4B)**, as you can see in `program4B.py`, we stored the _entire path_ (the list of indices) inside the DP table at _every single step_.
>     
> - The line `selectPath += path[i + k + 1]` performs list concatenation. In the worst case, this copy operation takes O(n) time. * Since this O(n) operation is _inside_ our main O(n) loop, the total time complexity for Algorithm 4 becomes **O(n2)**. 
>     
> 
> * **Algorithm 5** is our fully optimized **Θ(n)** solution. 
> 
> - The key difference is in `program5.py`. Instead of storing entire lists, we only store the max _value_ in the `var1` array.
>     
> - To build the path, we use a separate `pointer` array. At each step `i`, we just store a _single integer_ (an O(1) operation) pointing to the index we came from (`i-1` if we skipped, or `i-k-1` if we took). * _After_ the O(n) loop is finished, we run one final O(n) backward pass, just following the pointers to rebuild the final path. 
>     
> 
> So, the total time is O(n)+O(n), which is Θ(n). The lesson was that a small change in pathing—from list copying to back-pointers—was the difference between a quadratic and a linear algorithm."

---

#### Section 4: Implementation Demo (1.5 minutes)

**(Speaker: Shahyah)**

> "Now, I'll give a quick demo to prove this works. All our code is in standard Python.
> 
> **(Shares screen with a terminal/IDE)**
> 
> "Here is a simple test case: `n=4`, `k=1`, and `values = [1, 100, 101, 1]`. The clear optimal solution is to take vault 1 (value 1) and vault 3 (value 101), for a total of **102**.
> 
> First, let's run our 'smart' greedy **Algorithm 2**."
> 
> Bash
> 
> ```
> (echo 4 1; echo 1 100 101 1) | python program2.py
> ```
> 
> > **Output:** `101` `2` `4` "As you can see, Algorithm 2 fails. It picks 100 and 1 for a total of 101. It's **incorrect**.
> 
> Now, let's run the O(n2) **Algorithm 4B**."
> 
> Bash
> 
> ```
> (echo 4 1; echo 1 100 101 1) | python program4B.py
> ```
> 
> > **Output:** `102` `1` `3` "Algorithm 4B gets the **correct** answer.
> 
> Finally, our O(n) **Algorithm 5**."
> 
> Bash
> 
> ```
> (echo 4 1; echo 1 100 101 1) | python program5.py
> ```
> 
> > **Output:** `102` `1` `3` "Algorithm 5 also gets the **correct** answer. The demo shows that 4 and 5 are correct, but 2 is not. The plots will now show the speed difference."

---

#### Section 5: Experimental Results (1 minute)

**(Speaker: Sean)**

> "Looking at our experimental plots from the report, the difference becomes obvious.
> 
> **(Show 'Plot 7: Performance Comparison of All Algorithms')**
> 
> "This plot tells the whole story. * The blue line, **Program 3 (Recursive)**, is so slow it's just a dot at the origin; it couldn't handle the large input sizes. 
> 
> - The orange and green lines are **Program 4A and 4B**. You can see they have a distinct _curve_, which visually confirms our O(n2) analysis. Our 'Plot 8' also confirmed that the bottom-up 4B was consistently faster than the recursive 4A due to function call overhead. 
>     
> - And finally, the **red line is Program 5**. It is clearly the fastest, with a straight, linear slope. This plot is the practical proof that our O(n) optimization was successful."
>     

---

#### Section 6: Conclusion & Learning Experience (30 seconds)

**(Speaker: Shahyah)**

> "In conclusion, this project was a fantastic learning experience. We saw that greedy algorithms are fast but unreliable, and brute force is correct but unusable.
> 
> But the biggest takeaway, as I mentioned in my report, was the challenge of optimizing from Algorithm 4 to 5. It taught us that the algorithm design isn't finished at the recurrence. A small implementation detail—like list concatenation versus back-pointers —can be the critical difference between a slow quadratic algorithm and a fast, scalable linear one."

**(Speaker: Sean)**

> "Thank you for watching."