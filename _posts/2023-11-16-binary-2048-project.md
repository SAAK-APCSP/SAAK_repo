---
toc: false
comments: false
layout: post
title: Binary 2048 Project
description: :D
type: ccc
courses: { csp: {week: 13} }
---


<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
    }
    .grid-container {
      display: grid;
      grid-template-columns: repeat(4, 100px);
      grid-gap: 10px;
      margin: 20px;
    }
    .grid-item {
      width: 100px;
      height: 100px;
      text-align: center;
      line-height: 100px;
      font-size: 24px;
      border: 1px solid #ccc;
    }
  </style>
  <title>2048 Game</title>
</head>
<body>

<div id="score">Score: 0</div>
<div class="grid-container" id="grid-container"></div>

<script>
  document.addEventListener('DOMContentLoaded', function () {
    const gridSize = 4;
    const gridContainer = document.getElementById('grid-container');
    const scoreElement = document.getElementById('score');
    let score = 0;

    // Initialize the grid
    let grid = Array.from({ length: gridSize }, () => Array(gridSize).fill(0));

    // Add a random tile (2 or 4) to the grid
    function addRandomTile() {
      const availableCells = [];
      for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
          if (grid[i][j] === 0) {
            availableCells.push({ row: i, col: j });
          }
        }
      }

      if (availableCells.length > 0) {
        const randomIndex = Math.floor(Math.random() * availableCells.length);
        const randomCell = availableCells[randomIndex];
        const newValue = Math.random() < 0.9 ? 2 : 4;
        grid[randomCell.row][randomCell.col] = newValue;
      }
    }

    // Update the UI based on the grid state
    function updateUI() {
      gridContainer.innerHTML = '';
      for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
          const value = grid[i][j];
          const gridItem = document.createElement('div');
          gridItem.classList.add('grid-item');
          gridItem.textContent = value === 0 ? '' : value;
          gridContainer.appendChild(gridItem);
        }
      }
      scoreElement.textContent = `Score: ${score}`;
    }

    // Move tiles up
    function moveUp() {
      let moved = false;

      for (let j = 0; j < gridSize; j++) {
        for (let i = 1; i < gridSize; i++) {
          if (grid[i][j] !== 0) {
            let k = i;
            while (k > 0 && grid[k - 1][j] === 0) {
              // Move tile up
              grid[k - 1][j] = grid[k][j];
              grid[k][j] = 0;
              k--;
              moved = true;
            }
            if (k > 0 && grid[k - 1][j] === grid[k][j]) {
              // Merge tiles
              grid[k - 1][j] *= 2;
              grid[k][j] = 0;
              score += grid[k - 1][j];
              moved = true;
            }
          }
        }
      }

      return moved;
    }

    // Move tiles down
    function moveDown() {
      let moved = false;

      for (let j = 0; j < gridSize; j++) {
        for (let i = gridSize - 2; i >= 0; i--) {
          if (grid[i][j] !== 0) {
            let k = i;
            while (k < gridSize - 1 && grid[k + 1][j] === 0) {
              // Move tile down
              grid[k + 1][j] = grid[k][j];
              grid[k][j] = 0;
              k++;
              moved = true;
            }
            if (k < gridSize - 1 && grid[k + 1][j] === grid[k][j]) {
              // Merge tiles
              grid[k + 1][j] *= 2;
              grid[k][j] = 0;
              score += grid[k + 1][j];
              moved = true;
            }
          }
        }
      }

      return moved;
    }

    // Move tiles left
    function moveLeft() {
      let moved = false;

      for (let i = 0; i < gridSize; i++) {
        for (let j = 1; j < gridSize; j++) {
          if (grid[i][j] !== 0) {
            let k = j;
            while (k > 0 && grid[i][k - 1] === 0) {
              // Move tile left
              grid[i][k - 1] = grid[i][k];
              grid[i][k] = 0;
              k--;
              moved = true;
            }
            if (k > 0 && grid[i][k - 1] === grid[i][k]) {
              // Merge tiles
              grid[i][k - 1] *= 2;
              grid[i][k] = 0;
              score += grid[i][k - 1];
              moved = true;
            }
          }
        }
      }

      return moved;
    }

    // Move tiles right
    function moveRight() {
      let moved = false;

      for (let i = 0; i < gridSize; i++) {
        for (let j = gridSize - 2; j >= 0; j--) {
          if (grid[i][j] !== 0) {
            let k = j;
            while (k < gridSize - 1 && grid[i][k + 1] === 0) {
              // Move tile right
              grid[i][k + 1] = grid[i][k];
              grid[i][k] = 0;
              k++;
              moved = true;
            }
            if (k < gridSize - 1 && grid[i][k + 1] === grid[i][k]) {
              // Merge tiles
              grid[i][k + 1] *= 2;
              grid[i][k] = 0;
              score += grid[i][k + 1];
              moved = true;
            }
          }
        }
      }

      return moved;
    }

    // Check for game over
    function isGameOver() {
      for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
          if (grid[i][j] === 0) {
            return false; // There is an empty cell, game is not over
          }

          // Check adjacent cells for matching values
          if (
            (i < gridSize - 1 && grid[i][j] === grid[i + 1][j]) ||
            (j < gridSize - 1 && grid[i][j] === grid[i][j + 1])
          ) {
            return false; // There are matching adjacent cells, game is not over
          }
        }
      }
      return true; // No empty cells and no matching adjacent cells, game is over
    }

    // Listen for arrow key presses
    document.addEventListener('keydown', function (event) {
      if (!isGameOver()) {
        let moved = false;

        switch (event.key) {
          case 'w':
            moved = moveUp();
            break;
          case 's':
            moved = moveDown();
            break;
          case 'a':
            moved = moveLeft();
            break;
          case 'd':
            moved = moveRight();
            break;
        }

        if (moved) {
          addRandomTile();
          updateUI();
          if (isGameOver()) {
            alert('Game Over! Your score: ' + score);
          }
        }
      }
    });

    // Initial setup
    addRandomTile();
    addRandomTile();
    updateUI();
  });
</script>

</body>
</html>
