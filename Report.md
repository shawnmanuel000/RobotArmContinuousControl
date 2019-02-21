# Project Report

[image1]: Rewards.png "Rewards plot"

This report outlines the learning algorithm used to train the agent in the Continuous_Control.ipynb notebook as well as the performance of the agent as it was trained.

### Learning Algorithm

The agent was trained using the Deep Deterministic Policy Gradient (Actor Critic) learning algorithm implemented through neural networks. This algorithm uses two networks, an actor network for calculating the action to take in the given state, and a critic network for approximates the expected reward, `Q`, from the actor's action, `a`, in a state, `s`, according to the Bellman equation which is given as:

**`Q(s,a) = r + gamma * Q(s')`**

where `r` is the reward received from the action and `s'` is the next state.

At each timestep, the critic is trained first on the experiences to converge its estimates of the actor's value towards the q target of the Bellman equation. The actor is then trained according to the advantage of its predicted action compared to the critic's valuation of that action. Both networks had a similar structure of 3 hidden layers with 100 hidden nodes. Then a learning rate of 0.00025 was chosen to make small steps towards updating the network. Training the network was enhanced with experience replay with a replay buffer having size of 100000 and sampling 50 experience tuples each training step. This was to balance the lower learning rate and remove any temporal correlation between training samples.

Finally, the training process used an epsilon-greedy policy starting with epsilon = 1.0 at the start and then decaying at a rate of 0.99 to keep randomly exploring for the first 100 episodes until epsilon was capped at a minimum of 0.1. This was to ensure that the agent could still benefit from long term exploration.

### Plot of Rewards

The agent was trained for 200 episodes where the total reward for each episode (blue) and the average reward over the last 100 episodes (orange) is shown in the figure below. The x axis is the number of episodes and the y axis is the score. It can be seen that the agent reaches the average score of 35 after about 200 episodes.

![Rewards plot][image1]

### Future Work

From the plot, the agent's performance is fairly steady until it reaches the maximum reward of 40 and then it becomes unstable. For future work, the stability of the agent can be improved by implementing Proximal Policy Optimization for a more reliable policy update algorithm.

Finally, the agent can be enhanced to learn in parallel with asynchronous agents all adding experiences to the buffer to train on.