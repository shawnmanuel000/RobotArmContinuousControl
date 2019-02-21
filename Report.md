# Project Report

[image1]: Rewards.png "Rewards plot"

This report outlines the learning algorithm used to train the agent in the Navigation.ipynb notebook as well as the performance of the agent as it was trained.

### Learning Algorithm

The agent was trained using the Q-Learning algorithm implemented through neural networks. This algorithm approximates the expected reward, `Q`, from an action, `a`, in a state, `s`, according to the Bellman equation which is given as:

**`Q(s,a) = r + gamma * Q(s')`**

where `r` is the reward received from the action and `s'` is the next state.

Then the policy for selecting an action is to select the action with the highest expected reward for a given state. The neural network for approximating the Q values involves two hidden layers with 128 and 64 nodes and the relu activation. Then a learning rate of 0.0001 was chosen to make small steps towards updating the network. Training the network was enhanced with experience replay with a replay buffer having size of 50000 and sampling 50 experience tuples each training step. This was to balance the lower learning rate and remove any temporal correlation between training samples.

Finally, the training process used an epsilon-greedy policy starting with epsilon = 1.0 at the start and then decaying at a rate of 0.995 to keep randomly exploring for the first 300 episodes until epsilon was capped at a minimum of 0.1. This was to ensure that the agent could still benefit from long term exploration.

### Plot of Rewards

The agent was trained for 2000 episodes where the total reward for each episode (blue) and the average reward over the last 100 episodes (orange) is shown in the figure below. The x axis is the number of episodes and the y axis is the score. It can be seen that the agent reaches the average score of 13 after about 600 episodes.

![Rewards plot][image1]

### Future Work

From the plot, the agent's performance after reaching an average score of 13 is a bit unstable and drops below that a few times. For future work, the stability of the agent can be improved by implementing double DQNs where a target network is used for selecting actions and is updated slowly from the local network that is being trained. Another way to increase the efficiency of training is to use ensembles of Q-networks to reduce the variance of the q values calculated earlier on in training.

Finally, the agent can be enhanced to solve more complex problems such as being trained with the raw pixels of the environment as the state for an additional challenge.