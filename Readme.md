PROJECT NAME-Easy Algo Visualizer

> Terminal Maze Solver · 8 Algorithms · 4 Mazes · Pure Python · Zero Dependencies



## Overview

I basically made an Easy Algo Visualizer is a terminal-based, animated maze-solving program written in pure Python. It brings 8 classic search algorithms to life — each one rendered step-by-step in your terminal with real-time colour highlighting of explored cells, the active frontier, and the final discovered path.

Unlike web-based visualizers, this runs entirely offline with **zero dependencies** beyond Python's standard library. Every algorithm has a distinct colour identity and the display updates live as the solver works through the maze.



## Features

- **Animated Solvers** — 8 search algorithms with live step-by-step animation
- **4 Mazes** — hand-crafted layouts with unique difficulty and structure
- **Tournament Mode** — run all 8 algorithms silently and see a ranked leaderboard with 🥇🥈🥉
- **Speed Control** — adjustable animation delay from 0.0s (instant) to 1.0s (slow-motion)
- **Live HUD** — colour-coded cells: Start, Goal, Wall, Explored, Frontier, Path
- **No Dependencies** — uses only `collections`, `heapq`, `time`, `os`, `sys`

---

## Installation & Setup

### Requirements
- Python 3.8 or higher (uses walrus operator `:=`)
- A terminal that supports ANSI colour codes:
  - Windows: **Windows Terminal** (recommended) or PowerShell
  - macOS: Terminal or iTerm2
  - Linux: Any terminal

### Steps

1. Clone the repo or download `labyrinthian_v2.py`

```bash
git clone https://github.com/yourusername/easy-algo-visualizer
cd easy-algo-visualizer
```

2. Run the program — no pip installs needed:

```bash
python labyrinthian_v2.py
```
 If `python` is not recognized, try `python3`. Make sure Python was installed with **"Add to PATH"** checked.



## Controls

| Key | Action |
|-----|--------|
| `1` – `8` | Run the corresponding algorithm with live animation |
| `T` | Tournament mode — all 8 algorithms race, leaderboard shown |
| `M` | Switch the active maze |
| `S` | Set animation speed (e.g. `0.05` for fast, `0.15` for slow-motion) |
| `Q` | Quit |


## Algorithm Reference

| Algorithm | Data Structure | Optimal? | Time | Space | Notes |
|-----------|---------------|----------|------|-------|-------|
| BFS | Queue (FIFO) | ✅ Yes | O(V+E) | O(V) | Guaranteed shortest path |
| DFS | Stack (LIFO) | ❌ No | O(V+E) | O(depth) | Memory efficient, not optimal |
| A\* | Priority Queue | ✅ Yes | O(b^d) | O(b^d) | Best overall — uses heuristic |
| Dijkstra | Priority Queue | ✅ Yes | O((V+E)logV) | O(V) | Optimal for weighted graphs |
| Greedy | Priority Queue | ❌ No | O(b^m) | O(b^m) | Fast but can be fooled |
| Bidirectional | Two Queues | ✅ Yes | O(b^(d/2)) | O(b^(d/2)) | Searches from both ends |
| IDA\* | Recursive Stack | ✅ Yes | O(b^d) | O(d) | Optimal + memory lean |
| Beam | Bounded Queue | ❌ No | O(b·d) | O(b) | Fast, incomplete |



## Available Mazes

| Maze | Size | Description |
|------|------|-------------|
| Classic | 9×9 | Where legends begin. A balanced maze for testing all algorithms. |
| Vortex | 10×10 | Coiled like a serpent. Tests how algorithms handle spiral paths. |
| Deceiver | 10×10 | Bristling with dead-ends. Punishes Greedy, rewards BFS and A\*. |
| Tiny | 5×5 | Small but deadly. Great for understanding step-by-step flow. |

---

## Display Legend

| Symbol | Meaning |
|--------|---------|
| `S` | Start node |
| `G` | Goal node |
| `█` | Wall |
| `·` | Explored cell |
| `*` | Frontier (next to be explored) |
| `O` | Final path |



## Instructions for Testing

### Basic Run
1. Launch the program and press `1` to run BFS on the Classic maze
2. Watch the `·` cells expand outward ring by ring until the `O` path appears
3. Press Enter to return to the menu

### Compare Algorithms
1. Press `T` to enter Tournament mode
2. All 8 algorithms run silently on the current maze
3. A leaderboard appears — compare path length and cells explored
4. Notice how A\* and Bidirectional explore far fewer cells than BFS or Dijkstra

### Test a Hard Maze
1. Press `M` → select **Deceiver**
2. Run **Greedy** (`5`) — notice it struggles with dead-ends
3. Run **A\*** (`3`) on the same maze — compare the difference in explored cells



## Project Structure

```
labyrinthian_v2.py
│
├── Terminal & Colour     # RGB colour helpers, ANSI codes, cursor control
├── MAZES dict            # 4 hand-crafted grid layouts with start/goal/lore
├── nbrs / recon / mh     # Shared helpers: neighbours, path reconstruction, heuristic
├── render / show_frame   # Terminal renderer — draws grid, legend, and stats bar
├── gen_bfs … gen_beam    # 8 generator functions, each yields animation frames
├── ALGOS list            # Registry linking key names to generator functions
├── solve()               # Animates a single algorithm with adjustable delay
├── tournament()          # Runs all 8 silently, prints ranked leaderboard
└── menu() / main()       # Main loop — handles user input and routing
```


## Technologies Used

- **Language** — Python 3.8+
- **Standard Library** — `collections.deque` (BFS, Bidirectional), `heapq` (A\*, Dijkstra, Greedy, Beam)
- **Terminal Rendering** — ANSI escape codes with 24-bit RGB colour
- **Architecture** — Generator functions (`yield`) for frame-by-frame animation without threading
- **Dependencies** — None
.
