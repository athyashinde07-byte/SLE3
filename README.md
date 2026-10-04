# SLE-3: Architectural Design using Full C4 Model

**Course:** 02AML204 – Introduction to Artificial Intelligence
**Programme:** SY B.Tech. CSE (AI & ML) | Semester VI
**Name:** Atharv Deepak Shinde
**PRN:** 25UAM061
**Division:** A

---

## About This Project

SLE-3 documents the architecture of my SLE-2 system, the **BFS vs DFS Grid Search Profiling System**, using all four levels of the C4 model (Context, Container, Component, Code).

| SLE | Focus | Link |
|---|---|---|
| SLE-1 | Search / agent code | — |
| SLE-2 | Profiling BFS vs DFS (runtime and nodes expanded) | [SLE2-BFS-vs-DFS-Profiling](https://github.com/athyashinde07-byte/SLE2-BFS-vs-DFS-Profiling) |
| **SLE-3** | **Architecture design (full C4)** | This folder |

**System summary:** The system runs Breadth-First Search (BFS) and Depth-First Search (DFS) on a 40 x 40 open grid (start node `0`, goal node `1599`). It measures average runtime using Python `timeit` (5 batches x 100 repetitions) and counts the nodes each algorithm expands.

---

## C4 Model Overview

### Level 1 – Context
Shows the system and the outside world: the Student/Operator (user), Python `timeit` (external library) and GitHub (where code and report are published).

![Level 1 Context](images/level1_context.png)

### Level 2 – Container
Six main building blocks:

| Container | Responsibility |
|---|---|
| Grid Builder | Creates the 40 x 40 open grid as a graph (nodes 0–1599) |
| Search Engine | Runs BFS (queue) or DFS (stack) from start to goal |
| Visited Set | Stores visited nodes to avoid repeats and loops |
| Node Counter | Counts expanded nodes |
| Profiler | Uses `timeit` and computes mean and standard deviation |
| Report Output | Shows runtime and nodes-expanded results |

![Level 2 Container](images/level2_container.png)

### Level 3 – Component (Search Engine)
Internal parts of the Search Engine: **Frontier** (queue for BFS / stack for DFS), **Neighbours** (fixed expansion order), **Explored Set**, **Goal Test**, **Expansion Counter** and **Result Return**.

![Level 3 Component](images/level3_component.png)

### Level 4 – Code
Main classes and functions (names and responsibilities only):

| Name | Responsibility |
|---|---|
| `Grid` / `build_grid(n)` | Builds the n x n grid graph with neighbours |
| `bfs(graph, start, goal)` | Queue-based search; returns result and nodes expanded |
| `dfs(graph, start, goal)` | Stack-based search; returns result and nodes expanded |
| `visited` (set) | Stores explored node IDs |
| `expanded` (counter) | Counts expansions per run |
| `profile(func, repeat, number)` | `timeit` wrapper; returns mean and std dev (ms/run) |
| `main()` | Builds grid, profiles both algorithms, prints results table |

---

## Design Decisions

- Grid Builder, Search Engine and Profiler are separate so both algorithms run on exactly the same graph and neighbour order, keeping the comparison fair.
- Profiling is kept outside the search code so measurement does not change algorithm logic.
- A manual counter is used for nodes expanded because `timeit` only measures time.
- The Frontier is the only point where BFS and DFS differ, so the design is simple and can be extended (for example with A*) later.

---

## Repository Contents

```
SLE3/
├── README.md
├── AI_CONTRIBUTION_LOG.md
├── SLE3_25UAM061_AtharvShinde.docx    # Submitted report
└── images/
    ├── level1_context.png
    ├── level2_container.png
    └── level3_component.png
```

---

## AI Contribution

AI assistance was used for this SLE. See [AI_CONTRIBUTION_LOG.md](AI_CONTRIBUTION_LOG.md) for details.

---

## Note

The results quoted from SLE-2 (BFS expanded 1600 nodes and DFS expanded 79 nodes on this specific grid) apply only to that test case and are not a general claim that one algorithm is always faster.
