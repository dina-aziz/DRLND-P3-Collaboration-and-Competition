[image1]: training.PNG "training"
[image2]: average_scores_plot.PNG "plot"
# Project 2: Continuous Control  
    
## **Introduction**

#### The environment:      
For this project, the agent is trained to interact with the [Tennis](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#tennis) environment.
In this environment,  two agents control rackets to bounce a ball over a net.

#### The state space:    
The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket.Each agent receives its own, local observation.
#### The action space:    
Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping.   
#### The reward:       
 If an agent hits the ball over the net, it receives a reward of +0.1.  If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01.  Thus, the goal of each agent is to keep the ball in play.   
#### The environment solution:    
your agents must get an average score of +0.5 over 100 consecutive episodes, after taking the maximum over both agents.

## **The Learning Algorithm**

The learning algorithm used here is the Deep Deterministic Policy Gradients (**DDPG**) algorithm. The implementation is based on that of the [continuous control](https://github.com/dina-aziz/DRLND-P2-Continuous-Control) project. 

Detailed description of the DDPG can be found [here](https://arxiv.org/abs/1509.02971) and [here](https://spinningup.openai.com/en/latest/algorithms/ddpg.html).
### Implementation notes:    
- An agent uses four Vanilla networks as local/target actor(a deterministic policy network) and local/target critic(a Q-network) networks, each consists of 2 hidden layers of sizes 512 and 400 units respectively. 

- A replay buffer is used to let the agent remember and reuse experiences from the past. Here, a fixed length buffer of length 2x10^5 is used to store a finite number of experiences tuples
<s<sub>t</sub>,a<sub>t</sub>,r<sub>t+1</sub>,s<sub>t+1</sub>>.
    
- A minibatch of size 256 is sampled and used to train the agent. The samples of the minibatch are drawn from a uniform distribution in order to break any temporal/chronological relationship between them.

- Since the action space is continuous, exploring new actions occurs through adding Ornstein–Uhlenbeck Noise of parameters(mu = 0, theta = 0.15, sigma = 0.2)

- The learning step takes place every single iteration where the buffered experience tuples are sampled and used to train the networks. 
   
### A list if the hyperparameters used for training is provided below: 
   
- The replay buffer size: BUFFER_SIZE = int(2e5)    
- The minibatch size: BATCH_SIZE = 256
- The discount factor: GAMMA = 0.99 
- The target soft update parameter: TAU = 0.3 
- The number of training episodes: n_episodes = 2000    
#### Model Parameters:                
- The actor learning rate: LR_ACTOR = 5e-4         
- The actor first hidden layer size: fc1_units = 512   
- The actor Second hidden layer size: fc2_units = 400
- The critic learning rate: LR_CRITIC = 5e-4 
- The critic first hidden layer size: fcs1_units = 512   
- The critic Second hidden layer size: fc2_units = 400     
#### Ornstein–Uhlenbeck Noise Parameters:
- Noise parameters:
    - Mu = 0
    - Theta = 0.15
    - Sigma = 0.2      
         
### Results:
The training process was designed to proceed for 2000 episodes, where it can stop if the environment was solved (reached an average score of 0.5 over the last 100 episodes) in less episodes. In this case, the environment was solved in 679 episodes.   
 
  
![image1]

![image2]

### Future Ideas:
- **Implementing Prioritized Experience Replay.** 
- **Exploring other training algorithms such as:**    
1- Multi Agent Deep Deterministic Policy Gradients(MADDPG)  
2- Trust Region Policy Optimization (TRPO)  
3- Truncated Natural Policy Gradient (TNPG)   
4- Proximal Policy Optimization (PPO)   
5- Distributed Distributional Deterministic Policy Gradients (D4PG) 
  
 



 
