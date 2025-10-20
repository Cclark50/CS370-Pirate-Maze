# CS 370 Pirate Maze Game

## Briefly explain the work that you did on this project: What code were you given? What code did you create yourself?

From this project, I was given GameExperience.py, TreasureMaze.py, and the majority of the code in TreasureHuntGame - Christian Clark.ipynb. The code I created myself was most of the qtrain function in TreasureHuntGame - Christian Clark.ipynb. This function I created was to implement the Q-Learning algorithm so that the neural network that was created can learn how to navigate the given maze.

### Changes to GameExperience.py and TreasureMaze.py

Even though the requirements stated to not modify any code from GameExperience.py and TreasureMaze.py, I found some issues in those files that were preventing the neural network from learning properly.

#### Reward Changes

Originally, the reward for finishing the maze was set to a single 1.0. This was Far too low for the AI to learn from. This is because the step penalty was set to -0.04. Because of this, the break even point was only 25 (1.0 / 0.04) steps. past 25 steps a win will still give a negative score. I have determined that a reward of 6.0 is ideal, as it gives a break even point of 150 (6.0 / 0.04) steps. With a step limit of 75 and a reward of 6.0, the model will still have a positive score when winning even if it wanders with only -0.04 steps but this shouldnt ever happen as the neural network will still try to go to already traversed cells or invalid/blocked cells. This will, of course, require students to have a step limit set when training their model.

I have tested with a larger step limit and reward, but the results were the same. Training the model with a reward of 1.0 resulted in the AI never getting above a 35% win rate even after close to 10000 epochs and eventually converging on a loss of 0.000 with q values that were within 0.01 of eachother, meaning that all choices lead to bad outcomes as per the AI.

#### Bug fixes

-Major bug in get_data where the variable 'done' was being checked for the existance of itself and not if we're at a terminal state. Changing this mean that we can finally calculate the temporal difference at all, instead of always just calculating the reward. This is because checking for 'done' only checks to see if anything is inside the variable 'done' and not if we're at a terminal state.
-Major bug in update_state where when visiting the 'invalid' branch we were setting a variable 'mode' to invalid. This is incorrect as we want to set 'nmode' to invalid.

## What do computer scientists do and why does it matter?

Computer Scientists study computers and computer systems (Michigan Tech, 2025). Computer Scientists are neccesary to push the technological world forward to create new technology and algorithms to improve our work and lives. Without the Computer Scientists creating new and innovative programs and algorithms to take advantage of the innovations in hardware, technology would stagnate.

## How do I approach a problem as a computer scientist?

Personally, when I encoutner a problem I like to break down how the flow of the solution is supposed to look then define each step afterward. When I'm able to have this internal flowchart, I can then start to think about edge cases and other specifics that go into a solution. After having a very clearly defined plan, only then would I be able to start working on a concrete solution.

## What are my ethical responsibilities to the end user and the organization?

Ethics are extremely important in today's age of Artificial Intelligence. Keeping user's privacy safe and secure should be every organization's number one priority. Ignoring these priorities could open the organization up to lawsuits if we're unable to keep user's data and privacy safe. This also includes training our neural networks on ethically sourced data, as users could request for their data to be purged from our application and can cause huge headaches on trying to purge that data from a neural network.

## REFERENCES:

Michigan Tech. (2025). What is Computer Science?. Michigan Tech. https://www.mtu.edu/cs/what/.
