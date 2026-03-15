# TSP-Metaheuristics
This project explores different approaches for solving the Travelling Salesman Problem (TSP). The objective of the problem is simple to state: given a set of cities, find the shortest possible route that visits each city exactly once and returns to the starting point. Despite its simple formulation, the problem quickly becomes very difficult as the number of cities grows, which is why heuristic and metaheuristic methods are often used to find good approximate solutions.

The goal of this project was to implement and compare three different approaches: a simple greedy heuristic, and two metaheuristic algorithms. The greedy solution serves as a baseline, while the metaheuristics aim to improve upon it by exploring the search space more effectively.

The instances used in the experiments come from TSPLIB, a well-known collection of benchmark datasets for TSP research. Each instance provides the coordinates of a set of cities. From these coordinates, a distance matrix is computed using Euclidean distance, which is then used by the algorithms to evaluate the cost of a tour. (check dataset file)

The first approach implemented is the classic Nearest Neighbor greedy heuristic. Starting from a given city, the algorithm repeatedly moves to the closest unvisited city until all cities have been visited, and finally returns to the starting point. This method is extremely fast and easy to implement, but it often produces tours that are far from optimal because decisions are made purely based on local information. Still, it provides a useful baseline for comparison.

To obtain better solutions, two metaheuristic approaches were implemented. The first one is Particle Swarm Optimization (PSO). In this approach, a population of candidate solutions (called particles) explores the search space. Each particle represents a possible tour and iteratively updates its position based on both its own best solution and the best solution found by the swarm. Instead of initializing the particles randomly, the algorithm uses the greedy solution as a starting point and generates additional particles by applying small perturbations to it. This allows the swarm to start in a promising region of the search space rather than exploring completely random solutions. During the search process, a 2-opt local improvement step is occasionally applied to refine the tours.

The second metaheuristic implemented is Greedy Randomized Adaptive Search Procedure (GRASP). GRASP works in two phases. First, a solution is constructed using a randomized greedy strategy. Instead of always choosing the best next city, the algorithm builds a restricted list of good candidates and selects randomly from this list. This introduces diversity in the generated solutions and helps explore different parts of the search space. Once a complete tour is constructed, a local search procedure (again using 2-opt) is applied to improve it.

An important parameter in GRASP is α, which controls how greedy or how random the construction phase is. Smaller values make the algorithm behave more like a greedy method, while larger values allow more exploration. To study this effect, the algorithm was tested with three different values: α = 0.3, 0.4, and 0.5.

For each instance and each algorithm, the total tour cost and execution time were recorded. To evaluate the improvement of the metaheuristics compared to the greedy baseline, a relative gain metric was used:

Gain(%) = 100 × (C_greedy − C_meta) / C_greedy

This value indicates how much the metaheuristic improves the greedy solution in percentage terms.

Overall, the results show that while the greedy heuristic produces solutions almost instantly, the metaheuristic approaches consistently manage to reduce the tour cost. PSO benefits from starting with a good initial solution, which helps the swarm converge faster. GRASP, on the other hand, produces competitive results thanks to its balance between greedy construction and random exploration, especially when combined with local search.

In summary, this project highlights the trade-off between speed and solution quality when solving the TSP. Greedy heuristics provide quick baseline solutions, while metaheuristic methods such as PSO and GRASP require more computation but are capable of finding significantly better tours.
