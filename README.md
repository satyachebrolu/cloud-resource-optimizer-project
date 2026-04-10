# cloud-resource-optimizer-project

A C implementation of cloud task scheduling and allocation algorithms,
built as a Design and Analysis of Algorithms (DAA) course project.

## Problem Statement

Given a set of tasks (each with CPU, memory, and execution time requirements)
and a set of servers (each with a capacity and cost per CPU unit), allocate
every task to a server such that total cost is minimized and no server is
overloaded.

## Algorithms Implemented

### Phase 1 — Core Allocation
- **Greedy Allocator** — sorts tasks by CPU demand (largest first), assigns
  each to the server with the most free CPU that still fits the task.
  Time: O(n log n + n×m), Space: O(1)
- **Min-Heap Allocator** — same logic as Greedy but uses a max-heap ordered
  by free CPU to find the best server in O(log m) instead of O(m).
  Time: O(n log m), Space: O(m)

### Phase 2 — Optimization
- **DP Optimizer** — models each server as a knapsack. Builds a dp[i][j]
  table where each cell holds the minimum cost to assign i tasks across
  j servers. Provably optimal.
  Time: O(n×k), Space: O(n×k)
- **Comparison Engine** — runs Greedy and DP on identical input and prints
  a side-by-side cost and complexity comparison.

### Phase 3 — Advanced Features
- **Load Balancer** — implements and compares three policies:
  Round Robin (O(1)), Weighted Round Robin (O(k)), Least Connections (O(m))
- **SLA Checker** — flags tasks that exceed their deadline (finish time > deadline)
- **ASCII Gantt Chart** — prints a server × time grid showing which task
  runs on which server and when

## How to Build and Run

```bash
make
./allocator
```

Or compile manually:

```bash
gcc src/main.c src/task.c src/greedy.c src/heap.c \
    src/dp.c src/comparison.c src/loadbalancer.c \
    src/sla.c src/gantt.c -o allocator -lm
./allocator
```

## Sample Output

See `assets/sample_output.txt` for a full run with 8 tasks and 4 servers.

## Project Structure
cloud-task-allocator/
├── src/          ← all C source and header files

├── docs/         ← report and slides

├── assets/       ← sample output

├── Makefile

└── README.md

## Complexity Summary

| Algorithm         | Time              | Space   |
|-------------------|-------------------|---------|
| Greedy            | O(n log n + n×m)  | O(1)    |
| Min-Heap          | O(n log m)        | O(m)    |
| DP Optimizer      | O(n × k)          | O(n×k)  |
| Round Robin       | O(1) per task     | O(1)    |
| Weighted RR       | O(k) per task     | O(k)    |
| Least Connections | O(m) per task     | O(1)    |
| SLA Checker       | O(n)              | O(1)    |
| Gantt Print       | O(n × T)          | O(1)    |

## Author

Sai Satya Vani Chebrolu
