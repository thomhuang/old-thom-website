---
layout: page
title:  Conway's Game of Life
description: This is a python implementation of Conway's Game of Life,a no-player game, utilizing pygame and the implementation of sparse matrix.
---
<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>

I implemented <a href="https://github.com/thomhuang/Conway-s-Game-of-Life" target="_blank">Conway's Game of Life</a> as a little personal project that was inspired by first learning of it in Prof. Amit Sahai's CS 181 course. 

I utilized the `pygame` package in order to display the simulation and handle the graphics with ease, as well implementing the class `Board` that acts as a sparse matrix to replicate an infinite board for us to apply our algorithm to. We specifically utilized `Sprites` within `pygame` to represent each cell in our grid, allowing us to modify its color value individually depending on whether it's alive or not in the current generation.

The keybinds for the game are:
* **MOUSE**: If you click on any cell with any mouse event, changes cell from alive to dead or dead to alive pre-evolution.
* **ENTER**: Run a single evolution
* **BACKSPACE**: Resets the simulation

Below displays a current version of our grid (where white is an alive cell and black is a dead cell):

<img src="/assets/images/Conway.png" align="center">


