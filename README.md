# Kansas Route Finder - AI Search Algorithms

## Overview
This program implements five classic search algorithms from artificial intelligence and applies them to a real route-finding problem: finding a path between towns in Kansas using a road-adjacency graph and geographic coordinates.

Implemented algorithms:
- Breadth-First Search (BFS)
- Depth-First Search (DFS)
- Iterative-Deepening Depth-First Search (ID-DFS)
- Best-First (greedy) Search
- A* Search

The program reads town-to-town connections from `Adjacencies.txt` and town latitude/longitude from `coordinates.csv`, then lets the user pick a start town, a destination town, and a search algorithm from an interactive console menu.
For informed searches (Best-First and A*), the heuristic is the Euclidean distance between city coordinates, converted from degrees to kilometers.

## Why It Exists
This was written for CS 461 (Artificial Intelligence) as an assignment to implement and compare uninformed and informed search strategies on a non-trivial, real-world graph rather than a toy example.
Each search method reports how long it took to run and enforces a 10-second timeout, which makes the practical difference between the algorithms (especially DFS vs. BFS vs. A*) visible on the same dataset.

Development included the use of ChatGPT 4o as a coding assistant.
The full prompt-and-response log is preserved in `PROMPTS.md` for transparency; algorithm pseudocode was supplied by the assignment and given to the model, and the resulting code was tested and manually corrected (notably the distance-heuristic formula, which initially did not convert coordinate degrees to kilometers).

## How to Run
Requires a Java Development Kit (JDK 8+).

From the `SearchMethods` directory (so the program can find `Adjacencies.txt` and `coordinates.csv` via relative paths):

```bash
cd SearchMethods
javac -d bin src/routeFinder/*.java
java -cp bin routeFinder.RouteFinder
```

Follow the interactive prompts: enter a starting town, a destination town, and select a search algorithm (1-5) from the menu.
Town names must match the entries in `coordinates.csv` exactly (case-sensitive, underscores instead of spaces, e.g. `Bluff_City`).

## What It Demonstrates Technically
- Graph search with explicit open/closed sets over an adjacency-list representation
- FIFO queue (BFS), LIFO stack (DFS), and recursive depth-limited search with backtracking (ID-DFS)
- Priority-queue-based search ordered by a heuristic function (Best-First) and by combined path cost + heuristic (A*)
- A geographic distance heuristic that accounts for the non-uniform scale of longitude relative to latitude (cosine correction)
- Basic performance instrumentation (search timing in milliseconds) and a timeout safeguard for searches that fail to terminate quickly
