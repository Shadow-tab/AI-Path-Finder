# AI Path finder

AI 2002 - Artificial Intelligence | Assignment 1 | Spring 2026

A real-time interactive pathfinding visualizer built with Python and Pygame that demonstrates six fundamental uninformed search algorithms on a dynamic 10x10 grid. Watch each algorithm think step-by-step — frontier expansion, node exploration, dynamic obstacle re-planning, and the final path — all live.

---

## Features

- 6 Search Algorithms — BFS, DFS, UCS, DLS, IDDFS, Bidirectional Search
- Step-by-step visualization with color-coded frontier, explored, and path nodes
- Live data structure panel showing the actual Queue / Stack / Priority Queue updating every step
- Dynamic obstacles that spawn randomly every 3 seconds during search
- Auto re-planning if an obstacle blocks the current path the algorithm restarts instantly
- Clockwise movement order — Up, Right, Down, Down-Right, Left, Top-Left, Top-Right, Bottom-Left
- Click to toggle walls directly on the grid
- Speed control — Slow, Med, Fast, Max
- Animated final path with pulsing glow, directional arrows, and step index labels

---

## Project Structure

```
AI_A1_22F_XXXX/
|
|-- pathfinder.py        # Main application — all algorithms + GUI
|-- README.md            # This file
```

---

## Dependencies

| Package | Version | Purpose         |
|---------|---------|-----------------|
| Python  | 3.8+    | Runtime         |
| pygame  | 2.x     | GUI and visuals |

No other third-party libraries are required. All other modules used — collections, heapq, random, time, sys, math — are part of the Python standard library.

---

## Installation and Running

### Step 1 - Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/AI_A1_22F_XXXX.git
cd AI_A1_22F_XXXX
```

### Step 2 - Check Python version

Make sure Python 3.8 or higher is installed.

```bash
python --version
```

If not installed, download from https://www.python.org/downloads/

### Step 3 - Install Pygame

```bash
pip install pygame
```

If you have multiple Python versions installed:

```bash
pip3 install pygame
```

To install inside a virtual environment (recommended):

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate

pip install pygame
```

### Step 4 - Run the application

```bash
python pathfinder.py
```

The window will open immediately.

---

## How to Use

### Selecting an Algorithm

Click any of the six algorithm buttons at the bottom of the grid:

| Button | Algorithm               | Data Structure            |
|--------|-------------------------|---------------------------|
| BFS    | Breadth-First Search    | Queue (FIFO)              |
| DFS    | Depth-First Search      | Stack (LIFO)              |
| UCS    | Uniform-Cost Search     | Priority Queue (min-heap) |
| DLS    | Depth-Limited Search    | Stack with depth limit    |
| IDDFS  | Iterative Deepening DFS | Iteratively reset Stack   |
| Bidir  | Bidirectional Search    | Two Queues (fwd + bwd)    |

### Controls

| Control           | Action                          |
|-------------------|---------------------------------|
| START             | Begin the selected algorithm    |
| RESET             | Clear the search, keep walls    |
| NEW WALLS         | Regenerate a random wall layout |
| SLOW/MED/FAST/MAX | Control visualization speed     |
| Click grid cell   | Toggle a wall on or off         |

### Color Guide

| Color  | Meaning                                       |
|--------|-----------------------------------------------|
| Green  | Start node (S)                                |
| Blue   | Target node (T)                               |
| Red    | Static wall (-1)                              |
| Yellow | Frontier — nodes waiting in queue/stack       |
| Orange | Explored — nodes already popped and processed |
| Cyan   | Final path from S to T                        |

---

## Data Structure Panel

The panel on the right side of the grid shows the live contents of the algorithm's internal data structure, updated every single step.

- The green NEXT entry at the top is always the node about to be processed next
- For UCS, each entry shows its accumulated cost as g=X.X
- For DLS and IDDFS, each entry shows its current depth as d=X
- For Bidirectional, forward queue entries are tagged fwd and backward entries are tagged bwd

---

## Dynamic Obstacles and Re-planning

Every 3 seconds while a search is running, a random empty cell becomes a new obstacle shown in dark red. If this new obstacle lands on the currently planned path, the search automatically resets and re-plans from the start node using the updated grid with no user action required.

---

## Algorithm Notes

### Movement Order (Clockwise)

All algorithms expand neighbors in this strict clockwise order:

```
Up, Right, Down, Down-Right, Left, Top-Left, Top-Right, Bottom-Left
```

### Path Cost for UCS

- Cardinal move (Up, Right, Down, Left): cost = 1.0
- Diagonal move: cost = 1.414

### DLS Depth Limit

Default depth limit is 12. The current limit is shown live in the data structure panel header.

### IDDFS

Starts at depth limit 0 and increments by 1 each time the stack is exhausted. The current limit updates live in the panel header.

---

## Troubleshooting

**ModuleNotFoundError: No module named pygame**

```bash
pip install pygame
```

**Window does not open or crashes immediately**

Verify pygame installed correctly:

```bash
python -c "import pygame; print(pygame.version.ver)"
```

**On Linux - display errors**

If you see pygame.error: No available video device, install the SDL dependencies:

```bash
sudo apt-get install python3-pygame
```
