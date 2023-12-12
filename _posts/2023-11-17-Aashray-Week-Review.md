---
toc: false
comments: true
layout: post
title: Aashray Review
description: :D
type: ccc
courses: { csp: {week: 13} }
---

### 2048 
Using ChatGPT, we were able to create a funcitonal 2048 game.
1. Binary Shifting - We stored numbers in binary and used Javascript Binary Shifting (e.g. <<) to handle the powers of two.
2. By using for loops, we can iterate through all the rows and columns in the game board and update based on the inputs
3. Using functions, the different results of each input key can be emulated

See video

### Styling
Using .scss files, we were able to customize different aspects of the style
1. Page animation: Fade in transition for every page
2. Coloring: For the 2048 board game, we were able to color the boxes to any color we wanted

### Plans for the future
1. Add more to the styling to customize the frontend
2. Personalize the design of the page



Sure, here's a summary of the 2048 game implemented in the provided code in Markdown format:

## 2048 Game Summary

The 2048 game implemented in the provided code is a grid-based puzzle game where the player combines numbered tiles to reach the tile with the value 2048. Each move consists of shifting tiles in one of four directions: up, down, left, or right. The game incorporates binary concepts in the tile values, representing powers of 2.

### Grid Initialization

- The game starts with a 4x4 grid.
- Each cell in the grid can contain a tile with a value that is a power of 2 (2, 4, 8, 16, etc.).

### Adding Random Tiles

- The `addRandomTile` function randomly selects an empty cell in the grid and places a tile with a value of either 2 or 4.

### UI Update

- The `updateUI` function dynamically updates the HTML to reflect the current state of the grid.
- Each tile is displayed as a grid item with its value, and the color is determined by the value (with a special color for the value 2048).

### Moving Tiles

- The game allows the player to move tiles in four directions using the W (up), S (down), A (left), and D (right) keys.
- The movement functions (`moveUp`, `moveDown`, `moveLeft`, `moveRight`) handle the logic of shifting and merging tiles.

### Merging Tiles

- When tiles with the same value are moved into each other, they merge into a single tile with a value equal to the sum of the merged tiles.

### Scoring

- The player earns points each time tiles are merged. The score is displayed in the UI.

### Game Over

- The game checks for a "Game Over" condition by examining the grid.
- The game ends when there are no empty cells, and no adjacent cells have matching values.

### Binary Representation

- Although the code does not explicitly showcase binary representation, the game inherently uses binary principles by representing tile values as powers of 2 (2, 4, 8, 16, ...).
- The bitwise left shift operation (`<<`) is used when merging tiles, effectively doubling the value.

In summary, the 2048 game implemented in this code combines the binary concept of powers of 2 with a grid-based puzzle mechanic, challenging players to strategically merge tiles to reach the coveted value of 2048.





<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    @import 'SAAK_repo/_sass/minima/custom-styles';
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
    .number-color-2048 {
    color: #ff9800; /* Choose your desired color */
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
    // function updateUI() {
    //   gridContainer.innerHTML = '';
    //   for (let i = 0; i < gridSize; i++) {
    //     for (let j = 0; j < gridSize; j++) {
    //       const value = grid[i][j];
    //       const gridItem = document.createElement('div');
    //       gridItem.classList.add('grid-item');
    //       gridItem.textContent = value === 0 ? '' : value;
    //       gridContainer.appendChild(gridItem);
    //     }
    //   }
    //   scoreElement.textContent = `Score: ${score}`;
    // }

    // Update the UI based on the grid state
 function updateUI() {
    gridContainer.innerHTML = '';
    for (let i = 0; i < gridSize; i++) {
      for (let j = 0; j < gridSize; j++) {
        const value = grid[i][j];
        const gridItem = document.createElement('div');
        gridItem.classList.add('grid-item');
        gridItem.classList.add(`number-color-${value}`); // Add color class based on value
        gridItem.textContent = value === 0 ? '' : value;
        gridContainer.appendChild(gridItem);
      }
    }
    scoreElement.textContent = `Score: ${score}`;
  }


function restartGame() {
  // Reset the grid and score
  grid = Array.from({ length: gridSize }, () => Array(gridSize).fill(0));
  score = 0;
  // Add initial tiles
  addRandomTile();
  addRandomTile();
  // Update the UI
  updateUI();
}

// Function to get background color based on value

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
              grid[k - 1][j] = grid[k - 1][j] << 1;
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
              grid[k + 1][j] = grid[k + 1][j] << 1;
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
              grid[i][k - 1] = grid[i][k - 1] << 1;
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
              grid[i][k + 1] = grid[i][k + 1] << 1;
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




### Input output project.

Tasks:

Binary-to-Decimal Conversion:

Research and understand the binary-to-decimal conversion algorithm.
Implement a conversion function in the language of choice (e.g., JavaScript).
Test the conversion function with different binary inputs to ensure accuracy.
Basic User Interface:

Create a simple HTML form for binary input.
Implement a display area for showing the decimal output.
Use minimal styling with inline CSS for a clean appearance.
User Interaction:

Develop JavaScript functions to handle user input and update the display.
Include a "Convert" button to trigger the conversion process.
Deliverables:

Well-documented code for the binary-to-decimal conversion.
A basic HTML file for user input and result display.
Simple JavaScript functions for user interaction.



<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ASCII to Binary Emoji Converter</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            margin: 50px;
        }

        input, button {
            padding: 10px;
            font-size: 16px;
        }

        #output {
            margin-top: 20px;
            font-size: 18px;
        }
    </style>
</head>
<body>

    <h1>ASCII to Binary Emoji Converter</h1>

    <label for="messageInput">Enter a message:</label>
    <input type="text" id="messageInput" placeholder="Enter a message">

    <button onclick="convertToBinary()">Convert</button>

    <div id="output"></div>

    <script>
        const BITS_IN_BYTE = 8;

        function printBulb(bit) {
            if (bit === 0) {
                document.getElementById('output').innerHTML += "⚫";
            } else if (bit === 1) {
                document.getElementById('output').innerHTML += "🟡";
            }
        }

        function convertToBinary() {
            const message = document.getElementById('messageInput').value;

            document.getElementById('output').innerHTML = ""; // Clear previous output

            for (let i = 0; i < message.length; i++) {
                const decimal = message.charCodeAt(i);

                if (decimal === 0) {
                    printBulb(0);
                } else if (decimal !== 0) {
                    const bits = new Array(BITS_IN_BYTE).fill(0);

                    for (let j = BITS_IN_BYTE - 1; j >= 0; j--) {
                        bits[j] = decimal % 2;
                        decimal = Math.floor(decimal / 2);
                    }

                    bits.forEach(printBulb);
                    document.getElementById('output').innerHTML += "<br>"; // New line for a new set of 8 bulbs
                }
            }
        }
    </script>

</body>
</html>

