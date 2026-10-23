# Pirate Intelligent Agent: Deep Q-Learning Pathfinding

**PROSPER ASHANGA** | CS 370: Artificial Intelligence

## Overview

In this project, a pirate non-player character (NPC) learns to navigate an 8x8 maze and reach a treasure in the bottom-right corner, starting from any free cell. The pirate is never told the route. It learns by trial and error using deep Q-learning, which pairs a neural network with experience replay and a target network.

## Repository Contents

| File | Description |
|---|---|
| `Ashanga_Prosper_ProjectTwo.ipynb` | The completed Jupyter Notebook, with all training output saved |
| `TreasureMaze.py` | Provided environment class (maze, rewards, game status). Not modified |
| `GameExperience.py` | Provided experience-replay class (memory, sampling, Q-value targets). Not modified |
| `requirements.txt` | Python libraries needed to run the notebook |

## How to Run

1. Install the libraries: `pip install -r requirements.txt`
2. Open the notebook and choose **Run All** so the cells execute in order.
3. Training takes about 10 minutes on a CPU. The notebook then runs `completion_check()` and plays one full game from the top-left corner.

## Results

- The agent reached a 100% win rate and passed `completion_check()` at **epoch 402** (403 training games, 10.06 minutes).
- The first win came at epoch 4, the rolling win rate passed 0.9 at epoch 191, and it first reached 1.000 at epoch 214.
- Played from the starting cell (0,0), the trained pirate takes a 24-step path to the treasure, which is the shortest possible route in this maze.

## Project Reflection

### What code was I given, and what did I create?

I was given the environment (`TreasureMaze.py`), the experience-replay class (`GameExperience.py`), and a starter notebook. The notebook already included the 8x8 maze, the `show()` helper, `play_game()`, `completion_check()`, `build_model()` (a network with two 64-unit dense layers with PReLU and a four-unit output layer, one Q-value per move), `train_step()`, and the hyperparameters.

I created the Q-training algorithm inside `qtrain()`, which is the part marked `#TODO`. Each epoch starts the pirate in a random free cell. At every step the pirate either explores with a random valid move or exploits by choosing the highest predicted Q-value. The result is stored in the replay memory, and a random batch of 32 stored experiences trains the network. The target network is synchronized every 50 epochs. Training stops only when the win rate is at least 0.999 and `completion_check()` confirms a win from every starting cell. I commented the code in-line so it is readable and maintainable.

### What do computer scientists do, and why does it matter?

Computer scientists turn real problems into models a computer can work with, then design, build, test, and improve solutions. In this project that meant turning "find the treasure" into states, actions, and rewards, and then building an agent that learns a policy from them. It matters because software now sits inside systems people depend on, such as healthcare, finance, and transportation, so how well it is built and evaluated affects real people.

### How do I approach a problem as a computer scientist?

I start by defining the problem precisely and breaking it into parts. Then I build a simple baseline, implement the solution, and test it rigorously. This course showed me why that last step matters. In the pirate project, the rolling win rate reached 1.000 at epoch 214, but the agent did not win from every starting cell until epoch 402, so a good average had been hiding failures. I also compared approaches, such as value-based DQN on Cartpole against REINFORCE and A2C, and learned that each method has different strengths and costs. I document my work so that others, and my future self, can understand and reproduce it.

### What are my ethical responsibilities to the end user and the organization?

To the end user, I am responsible for safety, privacy, fairness, and honesty about what a system can and cannot do. That means collecting only the data that is needed, protecting it in line with laws such as HIPAA and GDPR, testing performance across groups instead of trusting one overall number, and keeping a human in control where mistakes could cause harm. To the organization, I am responsible for reporting results truthfully without overstating them, writing documented and maintainable code, and raising risks early instead of hiding them. The ACM Code of Ethics and Professional Conduct (2018) captures these duties, and I plan to follow it throughout my career, including as a future Physician Assistant working with AI tools in healthcare.
