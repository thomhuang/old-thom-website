---
layout: page
title:  Maze Solver
description: This is a python implementation of solving mazes, utilizing pygame and what I learned when building the application for Conway's Game of Life.
---
<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>

This is a python implementation of <a href="https://github.com/thomhuang/Maze-Solver" target="_blank">solving mazes</a>, utilizing pygame and what I learned when building the application for Conway's Game of Life. It implements the same idea of using `sprites` to represent each cell of our matrix/grid. 

In general a:

* **Green Cell**: Start cell
* **Red Cell**: Target cell
* **Grey Cell**: Wall cell
* **White Cell**: Visited cell

Where the keybinds for the game are:
* **s** : Places start node at mouse position
* **e** : Places target node at mouse position
* **LEFT CLICK**: While user holds left-click down, places walls continuously at mouse position until released
* **RIGHT CLICK**: While uesr holds right-click down, removes walls continuously at mouse position until released
* **BACKSPACE**: resets board to a empty board
* **d**: Performs depth first search
* **b**: Performs breadth first search

Below displays an example populated grid and depth-first search performed on the same grid:

<img src="/assets/images/maze1.png" align="center">

<img src="/assets/images/solved_maze1.png" align="center">


