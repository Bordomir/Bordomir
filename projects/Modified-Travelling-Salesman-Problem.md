# Modified TSP Solving Algorithms

This project implements a set of algorithms in C++ to solve a variation of the **Travelling Salesman Problem (TSP)**.
The problem requires finding the optimal set of closed paths in a weighted undirected graph that starts and ends at a specified node, while covering all other nodes under specific constraints.

## Repository

[Modified-Travelling-Salesman-Problem](https://github.com/Bordomir/Modified-Travelling-Salesman-Problem)

## Problem Description

Given:
- A **connected undirected simple graph** with `n` nodes (0 to n-1)
- **Weighted edges**
- A designated **main node** `m` (start and end of each path)
- A limit `k` ∈ [2, n-1] indicating the maximum number of unique nodes that can be **visited** in a single path

### Objective:
Find a set of **closed trails** starting and ending at node `m` such that:
- Every node (except `m`) is visited exactly once across all trails
- Each trail includes at most `k` visited nodes
- The total weight of used edges is minimized

## Mathematical Model

**Variables:**
- $x_{aij}$ – number of times edge between node `i` and node `j` is used in trail `a`
- $c_{ij}$ - weight of edge between node `i` and node `j`

**Objective Function:**  
$min\sum_{a}\sum_{i}\sum_{j>i}c_{ij}x_{aij}$

**Constraints:**
- Only valid edges used
- Each trail starts and ends at `m`
- Each node (except `m`) is visited exactly once
- No more than `k` visited nodes per trail

##  Project Components & Algorithms

### Data Generator (GDL)
Generates:
- A random connected graph with `n` nodes
- Random edge weights ∈ [1, edgeMaxWeight]
- Random main node `m` and random `k` ∈ [2, n-2]

Complexity:
- Time: O(n²)
- Space: O(n²)

### Greedy Algorithm (ALG)
Constructs trails by:
- Prioritizing edges with the lowest weight
- Trying to extend trails to unvisited nodes
- Ensuring the number of visited nodes doesn’t exceed `k`

Complexity:
- Time: O(n³)
- Space: O(n²)

### Greedy Randomized Algorithms (GR0, GR1, GR2)
Introduce randomness to the greedy algorithm:
- **GR0** – Randomize initial visited nodes
- **GR1** – Force inclusion (but not visit) of certain nodes in first trail
- **GR2** – Randomize node choices in all trails

Complexity:
- Time: O(n³)
- Space: O(n²)

### Metaheuristic Algorithm (AMH)
Combines results of:
- ALG + GR0/GR1/GR2 (multiple runs)
- Applies local search optimization
- Selects the best found solution

Complexity:
- Time: O(n⁴)
- Space: O(n²)

### Brute-Force Algorithm (ABF)
Finds the optimal solution:
- Enumerates all subsets of nodes of size ≤ k
- Uses modified Floyd-Warshall to find minimal paths
- Combines subsets to cover all nodes exactly once
- Uses **Branch & Bound** to reduce search space

Complexity:
- Time: O(2ⁿ)
- Space: O(2ⁿ × n)

## Example 

Input data:  
```
{
	"nodesNumber":	6,
	"mainNode":	0,
	"maxNodeVisitable":2,
	"graphMatrix":	[
				[-1, -1,  1,  1,  2,  1], 
				[-1, -1,  2, -1, -1, -1], 
				[ 1,  2, -1,  7, -1, -1], 
				[ 1, -1,  7, -1,  3,  9], 
				[ 2, -1, -1,  3, -1, -1],
				[ 1, -1, -1,  9, -1, -1]
			]
}
```
Representing graph:  
![image](https://github.com/user-attachments/assets/14a8a187-9f17-41cc-8fb3-7b6d0a3875bb)  
  
Output data:
```
{
	"result":	14,
	"trailsNumber":	3,
	"trailsLengths":[4, 3, 2],
	"trails":[
                        [[0, 2], [2, 1], [1, 2], [2, 0]],
                        [[0, 3], [3, 4], [4, 0]],
                        [[0, 5], [5, 0]]
                 ]
}
```
Representing 3 trails:  
![image](https://github.com/user-attachments/assets/6661b993-9413-4076-bfb9-6d60c1433b2a)  

## Experimental Results

### Test Setup
- 20 test cases (10 with n=5, 10 with n=10)
- Algorithms tested: ALG, GR0, GR1, GR2, AMH, ABF
- Measured: Solution quality (vs ABF) and computation time

### Key Insights:
- **ABF** always finds the optimal solution but is too slow for larger graphs
- **ALG** is fast and reliable
- **GR0-GR2** perform worse on average but can occasionally find near-optimal solutions
- **AMH** balances quality and performance effectively

### Diagrams

Average solution quality:  
![image](https://github.com/user-attachments/assets/87bb5957-3239-47e5-8202-ad797325d84b)  

Average computation time:  
![image](https://github.com/user-attachments/assets/1e374392-329d-40ca-b5ac-7116525e0ec3)

## Conclusion

- **Exact solution (ABF)** is suitable only for small graphs
- **Greedy (ALG)** is fast and simple, but not always optimal
- **Randomized (GR)** offer exploration at cost of consistency
- **Metaheuristic (AMH)** is the best compromise for practical use

## Source Files Overview

| Module              | Files                          | Description                                |
|---------------------|--------------------------------|--------------------------------------------|
| Data Generator      | `dataHolder.h/cpp`             | Generates random test graphs               |
| Greedy Algorithm    | `greedyAlgorithm.h/cpp`        | Core heuristic solver                      |
| Randomized Greedy   | `greedyRandomized[0-2].h/cpp`  | Adds randomness to greedy strategy         |
| Metaheuristic       | `metaheuristic.h/cpp`          | Combines and improves solutions            |
| Brute Force Solver  | `bruteForce.h/cpp`             | Exhaustive search for exact result         |

