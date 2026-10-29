# Constellation-Graphs
An interactive teaching tool that turns star constellations into graphs, interactively explore depth-first search (DFS), Dijkstra's algorithm and A* work through them one step at a time.  

Stars are nodes and the lines drawn between them are edges. Every constellation can be shown as an **undirected** or a **directed** graph, with **weighted** or **unweighted** edges.

It is a single self-contained HTML file. There is nothing to install and no build step.

## Features

- **15 constellations** with different graph shapes, so each algorithm meets a different challenge.
- **Undirected or directed edges.** In directed mode, click any line to cycle it between forward, reverse and both ways. "Reverse all" and "Reset directions" are provided.
- **Weighted or unweighted.** Weights come from the distance between stars on the chart. You can shuffle them to create new problems, or switch to unweighted.
- **Step-through traces** for DFS, Dijkstra and A\*, with Back, Next, Play and a step slider. The left and right arrow keys also step.
- **A plain-English note for every step**, explaining what the algorithm just did and why.
- **Live data structures:** the stack (DFS), the priority queue (Dijkstra) or the open and closed lists (A\*), plus a table of distances, g, h and f values and "came from" pointers.
- **A\* heuristic options:** straight-line distance, Manhattan distance, or none (h = 0). The page tells you whether the chosen heuristic is admissible for the current graph and goal.
- **Side-by-side comparison** of all three algorithms on the current graph: route, total cost and number of stars checked.
- **Pick your own start and goal** from the menus or by clicking stars on the chart.
- **Graph data export** for the current chart as an adjacency list, an adjacency matrix, or a ready-to-paste Python dictionary (with star coordinates for A\*).
- **Light and dark themes** that follow the system setting, and a layout that works from phone to desktop.

## The constellations

| Constellation | Shape | Useful for |
|---|---|---|
| Cassiopeia | A zig-zag path | A simple first graph |
| Ursa Major | A bowl cycle with a handle | Cycles plus a tail |
| Orion | Branching with a cycle | A good default for comparing all three algorithms |
| Leo | Two linked loops | Several competing routes |
| Pegasus | A cycle with a tail | Directed edges changing the answer |
| Crux | Two crossing lines with no shared star | **Disconnected graphs** and "no route found" |
| Cygnus | A hub with four spokes | High-degree nodes and DFS backtracking |
| Scorpius | One long curved path | A baseline where all three algorithms agree |
| Lyra | A four-star cycle with a tail | Cycles and visited sets |
| Gemini | A ladder | Many equal-cost routes and tie-breaking |
| Taurus | A branching tree | DFS going down the wrong branch |
| Sagittarius | A dense ring with chords | Many cycles; a clear Dijkstra versus A\* gap |
| Boötes | A kite | A cycle with a long tail |
| Draco | A long chain ending in a straight diagonal run | Showing a Manhattan heuristic overestimating |
| Ursa Minor | A bowl cycle with a handle | A mirror of Ursa Major |

**A note on accuracy:** star positions and magnitudes are simplified for teaching. They are not astronomical data, and in a few constellations the star order and spacing are stylised on purpose (Gemini's perfectly even ladder, for example).

## Running it

Open `index.html` in any modern browser. That is all.

To publish it with GitHub Pages:

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your main branch and the `/ (root)` folder, then save.
4. After a minute or so the page is live at `https://<your-username>.github.io/<repository-name>/`.

The page loads its fonts from Google Fonts. If that is blocked (on a school network, say), it falls back to system fonts and works the same.

## How it works

### Graph model

- Each constellation is a list of stars with `x` and `y` positions on a 0 to 100 grid, plus a list of lines between them.
- **Edge weight** is the straight-line distance between two stars divided by 5 and rounded up to a whole number, so weights are always positive integers. Shuffling adds a small random amount to each weight.
- **Directed mode** gives each edge a direction (forward, reverse or both). Undirected mode treats every edge as two-way.

### Algorithms

All three algorithms are written so that results are repeatable:

- **DFS** uses an explicit stack and tries neighbours in alphabetical order. It stops at the first route it finds, which is not always the cheapest.
- **Dijkstra** keeps a priority queue ordered by distance, and stops when the goal is settled. If a shorter route to an already settled star appears, that star is re-opened.
- **A\*** is Dijkstra ordered by `f = g + h`. Ties are broken by the lower `h`, then alphabetically.
- With no goal chosen, DFS and Dijkstra explore everything reachable from the start. A\* needs a goal.

### Heuristics

- **Straight line** is the distance between stars on the chart, scaled the same way as the weights. It never overestimates, so A\* is guaranteed to find a cheapest route. (preferable)
- **Manhattan** adds the horizontal and vertical differences. It can overestimate, so A\* may return a route that is not the cheapest. Draco is the best example.
- **None (h = 0)** makes A\* behave exactly like Dijkstra.

## Teaching ideas

- Run **DFS and Dijkstra on Orion** from A to H and compare the costs. Why DFS did not find the cheapest route?
- Switch **Sagittarius to directed**... What changed about the cheapest route? Why?
- On **Crux**, set the goal to a star in the other line. What does each algorithm report, and how their own code should handle it?
- On **Draco**, run A\* with straight-line and then Manhattan, and compare the routes.
- On **Gemini**, count how many routes have the same cost, and predict which one each algorithm will choose.
- Use **Unweighted** mode to show that DFS, Dijkstra and A\* ignore or use weights differently, and that Dijkstra then behaves like breadth-first search.
- Copy the **Python** export into a notebook and write your own search against the same data.

## Project layout

```
index.html   The whole app: markup, styles and script in one file
README.md    This file
```

## Licence

Released under the PolyForm Noncommercial License 1.0.0. See `LICENSE`.

Copyright (c) 2026 Richard Woodrow

