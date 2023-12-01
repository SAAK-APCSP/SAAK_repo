---
toc: false
comments: false
layout: post
title: Binary Art
description: :D
type: ccc
courses: { csp: {week: 14} }
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Platformer Game</title>
  <style>
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    #game-container {
      font-family: 'Courier New', Courier, monospace;
      font-size: 20px;
    }

    .row-input {
      margin-left: 10px;
    }
  </style>
</head>
<body>

<div id="game-container"></div>

<script>
  const numRows = 8;
  const numCols = 8;
  let gameGrid = [
    [0, 0, 1, 1, 1, 1, 0, 0],
    [0, 1, 1, 1, 1, 1, 1, 0],
    [1, 1, 1, 0, 0, 0, 0, 0],
    [1, 1, 1, 0, 0, 0, 0, 0],
    [1, 1, 1, 1, 1, 1, 1, 1],
    [1, 1, 1, 0, 0, 1, 1, 1],
    [1, 1, 1, 0, 0, 1, 1, 1],
    [1, 1, 1, 0, 0, 1, 1, 1]
  ];

  function renderGame() {
    const gameContainer = document.getElementById('game-container');
    gameContainer.innerHTML = '';

    for (let i = 0; i < numRows; i++) {
      const rowElement = document.createElement('div');
      const rowInput = document.createElement('input');
      rowInput.type = 'number';
      rowInput.value = parseInt(gameGrid[i].join(''), 2);
      rowInput.classList.add('row-input');
      rowInput.addEventListener('input', (event) => onRowInputChange(event, i));
      rowElement.appendChild(rowInput);

      for (let j = 0; j < numCols; j++) {
        const cell = document.createElement('span');
        cell.textContent = gameGrid[i][j] === 1 ? '#' : '.';
        rowElement.appendChild(cell);
      }
      gameContainer.appendChild(rowElement);
    }
  }

  function onRowInputChange(event, rowIndex) {
    const inputValue = parseInt(event.target.value, 10);
    const binaryString = inputValue.toString(2).padStart(numCols, '0');
    const inputArray = binaryString.split('').map(Number);

    if (inputArray.length <= numCols) {
      gameGrid[rowIndex] = inputArray;
    } else {
      alert(`Input length should not exceed ${numCols}`);
      event.target.value = parseInt(gameGrid[rowIndex].join(''), 2);
    }

    renderGame();
  }

  renderGame();
</script>

</body>
</html>
