## Reinforcement Learning
Is the structure of teaching an algorithm how to behave based on a reward function, a function that produces when the algorithm preforms correct actions for incorrect actions. This is different from supervised learning because we do not have the expected output. But rather an expected goal that the algorithm must learn.

We use a state and determine the reward factor of the algorithms performance. We try and teach to maximize the reward for the algorithm to follow.

### Return of reward
To encourage the algorithm to choose the most optimal reward, maybe not the best but the easiest to access. We can guide it to take the easiest route via a discount factor. The discount factor then is applied to the state causing larger/longer states to reward ratios to be reduced.

### Policy Function
A function that uses the reward to generate the best series of actions to follow.

### Q-function
Returns the optimal action to take. We try to max the Q function to then take the best actions.

