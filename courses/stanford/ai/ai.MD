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
