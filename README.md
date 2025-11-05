# CI2025_lab2
lab 2 Traveling Salesman Problem
-----

# 🇮🇹 Traveling Salesperson Problem (TSP) Solver: Italian Cities

This project implements a solution to the classic Traveling Salesperson Problem (TSP) using a **Genetic Algorithm (GA)** metaheuristic. The goal is to find the shortest possible route that visits 20 major Italian cities exactly once and returns to the starting city.

## ⚙️ Project Structure

The project consists of one file called **`tsp.ipynb`** that contains the full Genetic Algorithm (from EC) implementation and executes the solver.

## 🗺️ The Problem Data

The problem uses a $20 \times 20$ distance matrix derived from **real-world road distances (in kilometers)** between the following 20 Italian cities:

| Index | City | Index | City | Index | City | Index | City |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | Rome | 5 | Genoa | 10 | Venice | 15 | Taranto |
| 1 | Milan | 6 | Bologna | 11 | Verona | 16 | Brescia |
| 2 | Naples | 7 | Florence | 12 | Messina | 17 | Prato |
| 3 | Turin | 8 | Bari | 13 | Padua | 18 | Parma |
| 4 | Palermo | 9 | Catania | 14 | Trieste | 19 | Modena |

### ⚠️ Data Note: Triangle Inequality

The matrix, defined as `DISTANCE_MATRIX`, uses real world data about actual distances in kms from place A to place B. This matrix is **symmetric** (distance A to B equals B to A) but **does not strictly satisfy the Triangle Inequality**. This is common for real-world road networks, where geographical obstacles (mountains, coastlines) or specific highway layouts cause the distance through a third city to sometimes be shorter than the direct road distance.

## 🧬 Genetic Algorithm (GA) Implementation Details

The Genetic Algorithm is chosen because it offers a highly effective method for finding near-optimal solutions to large, computationally hard problems like the 20-city TSP, where brute-force methods are too slow.

### 1\. **Representation (Chromosome)**

  * A solution is represented as a **tour** (a list of 20 unique city indices), e.g., `[0, 5, 1, 3, ...]`.

### 2\. **Fitness Function**

  * The fitness of a tour is calculated as the **inverse of its total distance** ($\text{Fitness} = 1 / \text{Distance}$). The GA seeks to maximize fitness, which directly corresponds to minimizing the distance.

### 3\. **Selection (Tournament)**

  * **Tournament Selection** is used. In each step, a small number of individuals (`TOURNAMENT_SIZE=5`) are randomly sampled, and the one with the highest fitness (shortest distance) is chosen as a parent.

### 4\. **Crossover (Ordered Crossover - OX)**

  * The **Ordered Crossover (OX)** operator is used to combine two parent tours. This is essential for TSP because it ensures the offspring is always a **valid tour** (all cities visited once) by preserving the relative ordering of cities from the parents.

### 5\. **Mutation (Swap Mutation)**

  * **Swap Mutation** is applied to offspring with a small probability (`MUTATION_RATE=5%`). It randomly swaps the positions of two cities in the tour. This process introduces necessary randomness to help the algorithm avoid getting stuck in local minimums (sub-optimal solutions). It also garuantees that the best found result never degrades.

### Expected Output

The script will output the progress every 100 generations and provide the final, optimized tour sequence and its total distance in kilometers.

**Example Final Output:**

```
==================================================
Genetic Algorithm Optimization Complete
Final Best Tour Distance: 5018.00 km  (Actual value will vary slightly due to randomness)
==================================================
Optimal Tour (Sequence):
Rome -> Florence -> Prato -> Bologna -> Modena -> Parma -> Brescia -> Verona -> Venice -> Padua -> Trieste -> Milan -> Turin -> Genoa -> Naples -> Bari -> Taranto -> Palermo -> Messina -> Catania -> Rome
```
