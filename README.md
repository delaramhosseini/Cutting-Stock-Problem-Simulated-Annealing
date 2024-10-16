# Cutting Stock Problem Using Simulated Annealing

## Introduction
This project implements the **Simulated Annealing Algorithm** to solve the **Cutting Stock Problem**, an optimization challenge where the goal is to minimize material waste when cutting large rolls of material into smaller pieces to meet specific customer demands. The algorithm explores different cutting patterns and aims to find the most efficient one with minimal waste.

### Simulated Annealing Algorithm Overview

**Simulated Annealing** is a probabilistic optimization algorithm inspired by the process of annealing in metallurgy, where a material is heated and then slowly cooled to remove defects and optimize its structure. In optimization problems, it helps find an approximate global optimum by exploring the solution space more freely at higher temperatures and gradually narrowing down the search as the temperature decreases.

#### Key Steps in Simulated Annealing:
1. **Initial Temperature**: The algorithm starts with a high temperature, allowing it to accept both better and worse solutions in the beginning.
2. **Exploration**: At each step, a new neighbor solution is generated and compared to the current one. If the neighbor is better, it is accepted. If worse, it might still be accepted with a probability that depends on the current temperature and how much worse the solution is.
3. **Cooling**: As the temperature decreases over time, the algorithm becomes more selective, favoring better solutions and rejecting worse ones more often.
4. **Convergence**: Eventually, the temperature cools enough that the algorithm mostly accepts only better solutions, leading to convergence on a near-optimal solution.

#### Advantages:
- **Avoids Local Optima**: The ability to accept worse solutions early on helps the algorithm avoid getting stuck in suboptimal solutions (local minima).
- **Flexibility**: Simulated Annealing can be applied to a wide variety of optimization problems, including complex, non-convex problems.

#### Limitations:
- **Time Complexity**: The algorithm may take longer to converge compared to greedy algorithms or other methods, especially if the cooling rate is too slow.
- **Parameter Sensitivity**: The performance depends heavily on parameters like initial temperature, cooling rate (`alpha`), and stopping criteria.


## Project Structure

1. **Class Definition** (`Simulated_Annealing`):
   - The class `Simulated_Annealing` is designed to handle the optimization process. It initializes several instance variables, including:
     - `alpha`: The cooling rate (controls how quickly the temperature decreases).
     - `temperature`: The initial temperature for the annealing process.
     - `number_of_requests`: The total number of requests for specific material lengths.
     - `list_of_requests`: The list of requested lengths.
     - `length_of_roll`: The length of each roll of material.
     - `current_answer`: Represents the current cutting solution.
     - `current_fitness`: The number of rolls used in the current solution.
     - `neighbors`: A list of neighboring solutions (alternative cutting patterns).
     - `expected_number_of_rolls`: The optimal number of rolls that minimizes waste.
     - `maximum_iterations`: The maximum number of iterations allowed for the algorithm.

2. **Input Function** (`input`):
   - This function reads data from a specified file and stores it in instance variables. The file contains:
     - The length of the roll.
     - A list of customer requests (desired material lengths).
     - The expected number of rolls for optimal cutting.

3. **Initialization Function** (`initialize`):
   - This function initializes various instance variables based on the input data. It generates:
     - The list of requests.
     - The current solution (`current_answer`), which is initialized using the `initial_index_of_request` function.
     - The current fitness value (`current_fitness`), which is computed using the `fitness_function`.

4. **Initial Index of Request Function** (`initial_index_of_request`):
   - This function generates an initial arrangement of the requests by selecting indexes from both the beginning and the end of the list. If the number of requests is odd, the last index is excluded.

5. **Fitness Function** (`fitness_function`):
   - The fitness function calculates the quality of a cutting solution. It does this by:
     - Summing the requested lengths in the current cutting.
     - Using a new roll whenever the total exceeds the roll length.
     - Counting the number of rolls used and returning that value as the fitness score.

6. **Create Neighbors Function** (`create_neighbours`):
   - This function generates neighboring solutions by creating a deep copy of the current solution (`current_answer`) and swapping two random elements in the list to create a new solution. This new solution is returned as a neighbor.

7. **Next State Function** (`next_state`):
   - The `next_state` function generates a new potential solution using the Simulated Annealing algorithm. It:
     - Creates a new neighbor and calculates its fitness.
     - Computes the energy difference (`deltaE`) between the current solution and the neighbor.
     - If the neighbor's fitness is better (i.e., `deltaE < 0`), the current solution is updated with the neighbor.
     - If the neighbor’s fitness is worse, the solution might still be updated based on a probability calculated using the temperature and `deltaE`. This allows the algorithm to explore suboptimal solutions early on to avoid getting trapped in local optima.

8. **Run Function** (`run`):
   - The main loop of the Simulated Annealing algorithm. It:
     - Iteratively generates new states using the `next_state` method.
     - Continues until the maximum number of iterations is reached or the current solution matches or exceeds the expected number of rolls.
     - Reduces the temperature after each iteration according to the cooling rate (`alpha`), allowing the algorithm to gradually focus on more optimal solutions.
