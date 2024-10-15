# Cutting_Stock_Problem_Simulated_Annealing
1) The class Simulated_Annealing is defined. The constructor initializes various instance variables, including the alpha (cooling rate), temperature, number of requests, list of requests, length of a roll, current answer (representing the cutting of rolls), current fitness (number of rolls used), list of neighbors (possible solutions), expected number of rolls, and maximum number of iterations.

2) The input function takes a file path as input and reads the necessary data from the file. The data includes the length of a roll, a list of requests, and the expected number of rolls. This data is stored in instance variables for later use.

3) The initialize function initializes the instance variables based on the input data. It sets the requests, length of a roll, expected number of rolls, number of requests, current answer (initialized with an initial index of requests), and current fitness (calculated using the fitness function).

4) The initial_index_of_request function generates an initial index for the requests. It initializes the index list with pairs of indexes (one from the beginning and one from the end of the list of requests). If the number of requests is odd, it excludes the last index from the initial indexes.

5) The fitness_function function calculates the fitness of a cutting (represented by the suggested cutting). It iterates over the indexes in the suggested cutting, incrementing the current sum of pieces. If the sum exceeds the length of a roll, a new roll is used, and the used_rolls counter is incremented. The method returns the total number of rolls used.

6) The creat_neighbours function generates a list of neighboring cuttings. It creates a deep copy of the current answer and randomly swaps two elements in the copy to create a new neighbor. This new neighbor is returned.

7) The next_state function generates a new state from the current state using the Simulated Annealing algorithm. It creates a new neighbor, calculates the fitness of the neighbor, and calculates the energy difference (deltaE) between the neighbor and the current state. If deltaE is less than zero, indicating an improvement in fitness, the current state is updated with the neighbor. Otherwise, a random number is generated, and if it is less than the probability defined by the temperature and deltaE, the current state is still updated with the neighbor.

8) The run function is the main loop of the Simulated Annealing algorithm. It iteratively generates new states using the next_state method until either the maximum number of iterations is reached or the fitness of the current state becomes equal to or less than the expected number of rolls. The temperature is decreased at each iteration according to the cooling rate alpha.
