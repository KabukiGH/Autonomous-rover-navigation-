# Autonomous-rover-navigation-
Decision making algorithm base crowdsourcing knowledge
Main goal of the task was to design a decision-making mechanism to enable autonomous an autonomous agent to take advantage of the opportunities offered by crowdsourcing in a navigation task. The project is exactly focused on designing a navigation algorithm for an autonomous rover that needs to navigate an uncertain environment.

WP1: analyze and understand the supporting code on elearning.
The setup is as follows: an agent wants to navigate a 3-square wide grid, from bottom left to top right. The fields are numbered from 0 to 9. The middle square is an obstacle, represented by a very negative reward. The goal is to compare sources, coded as probability mass functions (pmfs), in order to select the best one at each step. For convenience, instead of using the whole state space as support for the pmfs, we reduce it to five possible actions: stay in place, move left, upwards, right downwards. The same principle was applied to reward lists.

• FindWall(x)
Function is used to distinguish the walls so that the robot does not travel beyond the edge of the grid. Function takes as an input the current position ot the agent, as an int value and returns an int list for each wall.

• Return_target(x)
Function is used to determine the target behavior of the agent. The function specified the diagonal of the grid from the start box to the target position. Fields below the diagonal specified the target behavior as going up, while fields above the diagonal specified it as going right. Thus, in a situation where there were no obstacles in the field, the agent would take the shortest path. Function takes as an input integer value equivalent to the square where agent is and returns the pmf corresponding to the target for this square.

• Return_reward(x)
Reward function takes as an input the position ot the agent, as an int value and returns reward, voded as a list of int values for current square. Square zero (the starting point) has a reward of -1, and square 4 (the middle) has a reward of -100. The rest of the squares have reward equal 0.

• Return_sources(x)
This function return the behavior of the sources for square x, where x is an input with a value of integer type. For each behavior, the function returns the corresponding pmf values. Then it calls the function FindWall(x). If the agent is at the wall, the corresponding move is replaced by "stay in place". The function returns a 4x5 matrix.

• DKL(l1,l2)
The source code also contains the DKL function, or Kullback-Leibler divergence, which is a measure of how one probability distribution is different from a second, reference probability distribution. As an input it takes 2 values and returns one value of float type.

WB2 Implement the greedy version of the algorithm
The problem is the uncertain environment in which the robot moves, containing obstacles. The agent must be able to collect information from third parties and re-use such information to achieve the destination. The agent must be also able to avoid obstacles in an uncertain surface.
A greedy algorithm was used to program the robot, which, in order to determine the solution at each step, makes the most promising partial solution choice at that time. It used the sources collected, compared with the target behaviour and analysed taking into account the cost function.
New features used in the algorithm:
• New_state(position, action)
The function takes as input the current position of the agent and the action number and returns the new state, depending on the planned action, where as action is considered: 0 - stop, 1 - move left, 2 - move up, 3 - move right, 4 - move down.
• Control_algorithm(actual_position)
Shown in figure 2.1.
• Loop(actual_position)
Used to obtain numerical simulation.

WB3 Obtain numerical simulations to illustrate the results
The Greedy algorithm is not a predictive algorithm, but in the case of a small grid it proved sufficient for the agent to reach the target, regardless of the location of the obstacle. To illustrate results performed a numerical and graphical simulation, library "Pygame" was used to represent the graphical results

WP4: Implement routines to scale-up the problem to larger grids
Extended verison of the project allows the user to generate an arbitrarily large grid and random obstacle’s positions or declare obstacles on specific fields. A size of grid is defined by user. In this version of the algorithm, the return_target(x) function has been modified to be universal, regardless of the grid size, but considers the grid as square. It uses the new target_direction() function, which contains all the calculations. Also modified the return_reward() function to be independent of the number of obstacles. To make the algorithm work properly, it was decided to write new function:
• Rand_obstacle_location()
The function draws obstacles at random locations. The number of obstacles depends on the size of the grid and is given by the formula:
numer_of_obstacles = grid_dimension – 2
• Simulation()
This function was imported from the Simulation.py file to run the graphical simulation. It takes as input the dimension of the grid, the fields with obstacles and the subsequent movements of the agent.

WB5: implement a receding horizon version of the algorithm
In this section the receding horizon version of the algorithm is implemented, which is a predictive algorithm. A property of predictive control is its repetitive mode of operation. It is possible to determine a sequence of future controls, but only the first step of this sequence is used, so that in the next step the whole calculation is repeated. In the main loop, we calculate the weights for control through a receding horizon and choose a policy. The idea is that we restric the state space to the relative states available to us and use crowdsourcing on this new state space. The function receding_horizon_crowdsourcing() takes as an input the value of prediction horizon and actual location of the agent and returns the corresponding policy.
