## MDP

In Deterministic Search:

"One outcome per action" means that from any state s, taking action a always leads to exactly one specific next state s'
The transition function is written as: s' = f(s,a)
This function is deterministic - it returns exactly one state

In MDPs:

"Multiple possible outcomes per action" means taking action a from state s could lead to different possible next states
The transition function is written as: P(s'|s,a)
This function is probabilistic - it returns a probability distribution over possible next states.
Se sono nello stato S  ed eseguo a non è detto che io finisca in S1. Ci sta che con una probabilità P1 io vada in S2 e con una P2 in S1.


Got it ✅ Let me give you a **clean resume in English** with all the key points about **$V$ and $Q$** in MDPs.

---

# 📌 State-value $V$ and Action-value $Q$ in MDPs

---

### 🔹 **State-value function $V(s)$**

* **Definition:**
  The expected return (cumulative reward) starting from state $s$ and following a policy $\pi$.

* **Formula:**

$$
V^\pi(s) = \mathbb{E}\Big[\sum_{t=0}^{\infty} \gamma^t R_{t+1} \ \Big| \ s_0 = s, \pi\Big]
$$

* **Meaning:** “How good is it to be in this state, assuming I act according to policy $\pi$?”

---

### 🔹 **Action-value function $Q(s,a)$**

* **Definition:**
  The expected return starting from state $s$, taking action $a$, and then following policy $\pi$.

* **Formula:**

$$
Q^\pi(s,a) = \mathbb{E}\Big[\sum_{t=0}^{\infty} \gamma^t R_{t+1} \ \Big| \ s_0=s, a_0=a, \pi\Big]
$$

* **Meaning:** “How good is it to take this action in this state, if afterwards I follow policy $\pi$?”

---

### 🔹 **Relationship between $V$ and $Q$**

* State value is the maximum (or expectation under policy) of action values:

$$
V^\pi(s) = \sum_a \pi(a|s)\, Q^\pi(s,a)
$$

* For the optimal case:

$$
V^*(s) = \max_a Q^*(s,a)
$$

---

### 🔹 **Example (Gridworld, state (3,1))**

* If the agent chooses **Left** at (3,1):

$$
Q((3,1), \text{Left}) = 0.8[r+V(2,1)] + 0.1[r+V(3,2)] + 0.1[r+V(3,1)]
$$

* If the agent chooses **Up** at (3,1):

$$
Q((3,1), \text{Up}) = 0.8[r+V(3,2)] + 0.1[r+V(2,1)] + 0.1[r+V(4,1)]
$$

* The state value is then:

$$
V(3,1) = \max \{ Q((3,1),\text{Left}), \ Q((3,1),\text{Up}), \ Q((3,1),\text{Right}), \ Q((3,1),\text{Down}) \}
$$

---

✅ **Summary:**

* $V(s)$ = **value of being in a state**.
* $Q(s,a)$ = **value of being in a state and taking an action**.
* Relation: $V(s) = \max_a Q(s,a)$.
* Both are **expected values** (averages over possible stochastic outcomes).

---

Great—here are two quick, concrete examples you can copy-paste into notes.

# 1) Tiny MDP (no grid), numbers worked out

* States: **s** (non-terminal), **G** (terminal +1), **B** (terminal –1)
* Discount: $\gamma=1$
* Per-step reward in non-terminal moves: $r=0$

From **s**:

* **Action A:** $P(G|s,A)=0.8,\ P(B|s,A)=0.2$
* **Action B:** $P(G|s,B)=0.6,\ P(B|s,B)=0.4$

Because terminals pay immediately and then stop:

$$
Q(s,A)=0.8\cdot(+1)+0.2\cdot(-1)=0.6
$$

$$
Q(s,B)=0.6\cdot(+1)+0.4\cdot(-1)=0.2
$$

$$
V(s)=\max\{Q(s,A),Q(s,B)\}=0.6
$$

**Takeaway:** $V(s)$ is the best action’s $Q$; each $Q$ is an **expected value** over outcomes.

---

# 2) Gridworld-style one-state example (mirrors Russell–Norvig)

Suppose we’re in state $s=(3,1)$. If we choose **Left** the stochastic model is:

* 0.8 → to $(2,1)$
* 0.1 → to $(3,2)$
* 0.1 → stays in $(3,1)$ (bump into wall)

Let the step reward be $r=-0.04$, $\gamma=1$, and assume we already computed state values

$$
V(2,1)=0.6953,\quad V(3,2)=0.7003,\quad V(3,1)=0.6514.
$$

Then

$$
\begin{aligned}
Q((3,1),\text{Left})
&=0.8\,[r+V(2,1)] + 0.1\,[r+V(3,2)] + 0.1\,[r+V(3,1)]\\
&=0.8(-0.04+0.6953) + 0.1(-0.04+0.7003) + 0.1(-0.04+0.6514)\\
&\approx 0.6514.
\end{aligned}
$$

If instead we choose **Up** (0.8 to $(3,2)$, 0.1 to $(2,1)$, 0.1 to $(4,1)$ with $V(4,1)=0.4279$):

$$
\begin{aligned}
Q((3,1),\text{Up})
&=0.8\,[r+V(3,2)] + 0.1\,[r+V(2,1)] + 0.1\,[r+V(4,1)]\\
&\approx 0.6325.
\end{aligned}
$$

Finally,

$$
V(3,1)=\max_a Q((3,1),a)=\max\{Q_\text{Left},Q_\text{Up},Q_\text{Right},Q_\text{Down}\}.
$$

**Key points recap**

* $V(s)$: **state-value function** = expected return from $s$ under a policy.
* $Q(s,a)$: **action-value function** = expected return from $s$ if you take $a$, then follow the policy.
* Relationship: $V^\pi(s)=\sum_a \pi(a|s)Q^\pi(s,a)$; in the optimal case $V^*(s)=\max_a Q^*(s,a)$.
* The 0.8 / 0.1 / 0.1 are the **transition probabilities** used to form the expected value.

Great—here’s the derivation in small, clean steps from the **definition of $Q^\pi$** to the **Bellman equation for $Q^\pi$**.

---

## 1) Start from the definition

$$
Q^\pi(s,a)\;=\;\mathbb{E}\!\left[\sum_{t=0}^{\infty}\gamma^{t}R_{t+1}\ \Big|\ s_0=s,\;a_0=a,\;\pi\right].
$$

This is the expected discounted return if we start in $s$, **take action $a$ now**, and then follow policy $\pi$.

---

## 2) Split off the first reward

Separate the sum into the **immediate** reward and the **rest**:

$$
\sum_{t=0}^{\infty}\gamma^{t}R_{t+1}
\;=\;R_{1}\;+\;\gamma\sum_{t=1}^{\infty}\gamma^{\,t-1}R_{t+1}.
$$

Therefore

$$
Q^\pi(s,a)
=\mathbb{E}\!\left[R_1\ \Big|\ s_0=s,a_0=a\right]
+\gamma\;\mathbb{E}\!\left[\sum_{t=1}^{\infty}\gamma^{\,t-1}R_{t+1}\ \Big|\ s_0=s,a_0=a,\pi\right].
$$

---

## 3) Condition on the next state $s_1$ (law of total expectation)

Insert a sum over all possible next states:

$$
\mathbb{E}\!\left[\cdot\ \Big|\ s_0=s,a_0=a\right]
=\sum_{s'}P(s_1=s'\mid s_0=s,a_0=a)\;\mathbb{E}\!\left[\cdot\ \Big|\ s_0=s,a_0=a,s_1=s'\right].
$$

Apply this to the two expectations:

### (a) Immediate term

With the standard MDP reward model $R(s,a,s')=\mathbb{E}[R_1\mid s_0=s,a_0=a,s_1=s']$,

$$
\mathbb{E}[R_1\mid s_0=s,a_0=a]
=\sum_{s'}P(s'|s,a)\;R(s,a,s').
$$

### (b) Future term

After we reach $s_1=s'$, we will act according to the policy $\pi$.
By definition of the **state-value function** under $\pi$,

$$
V^\pi(s')=\mathbb{E}\!\left[\sum_{t=1}^{\infty}\gamma^{\,t-1}R_{t+1}\ \Big|\ s_1=s',\pi\right].
$$

Hence,

$$
\mathbb{E}\!\left[\sum_{t=1}^{\infty}\gamma^{\,t-1}R_{t+1}\ \Big|\ s_0=s,a_0=a\right]
=\sum_{s'}P(s'|s,a)\;V^\pi(s').
$$

---

## 4) Put it together

Combine (a) and (b):

$$
\boxed{
Q^\pi(s,a)
=\sum_{s'} P(s'|s,a)\,\Big[\,R(s,a,s')+\gamma\,V^\pi(s')\Big].
}
$$

This is the **Bellman expectation equation** for the action-value function.

---

## 5) Optimal case

If $\pi$ is optimal, replace $V^\pi$ and $Q^\pi$ by $V^*$ and $Q^*$, and note

$$
V^*(s)=\max_{a'} Q^*(s,a').
$$

Substituting gives the **Bellman optimality equation** for $Q$:

$$
\boxed{
Q^*(s,a)=\sum_{s'} P(s'|s,a)\,\Big[\,R(s,a,s')+\gamma\,\max_{a'} Q^*(s',a')\Big].
}
$$

---

### Notes/assumptions (standard in MDPs)

* **Markov property:** transitions depend only on current $s,a$.
* Reward written as $R(s,a,s')$ (can be any equivalent formulation).
* If $s'$ is terminal, typically $V^\pi(s')=0$ and only the terminal reward contributes.
* Discount $\gamma\in[0,1)$ (or $\gamma=1$ in episodic tasks with finite expected return).

That’s the full derivation from definition → Bellman form.

