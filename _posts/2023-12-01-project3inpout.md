---
toc: false
comments: false
layout: post
title: Input Output
description: :D
type: ccc
courses: { csp: {week: 13} }
---

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





