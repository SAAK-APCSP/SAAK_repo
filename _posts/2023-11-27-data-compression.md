---
toc: false
comments: false
layout: post
title: Binary 2048 Ideation and Planning
description: :D
type: ccc
courses: { csp: {week: 13} }
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Run-Length Encoding (RLE) Compression</title>
</head>
<body>

<script>
  function compress(inputString) {
    let compressedData = "";
    let count = 1;

    // Iterate through the input string
    for (let i = 1; i < inputString.length; i++) {
      if (inputString[i] === inputString[i - 1]) {
        count++;
      } else {
        compressedData += inputString[i - 1] + count;
        count = 1;
      }
    }

    // Add the last character and its count
    compressedData += inputString.slice(-1) + count;

    return compressedData;
  }

  function decompress(compressedData) {
    let decompressedData = "";

    // Iterate through the compressed data
    for (let i = 0; i < compressedData.length; i++) {
      let char = compressedData[i];
      let countStr = "";

      // Extract the count value
      i++;
      while (i < compressedData.length && !isNaN(parseInt(compressedData[i]))) {
        countStr += compressedData[i];
        i++;
      }

      let count = parseInt(countStr);

      // Repeat the character count times
      decompressedData += char.repeat(count);
    }

    return decompressedData;
  }

  // Example usage
  let originalData = "AAAABBBCCDAA";
  let compressedData = compress(originalData);
  let decompressedData = decompress(compressedData);

  console.log("Original data:", originalData);
  console.log("Compressed data:", compressedData);
  console.log("Decompressed data:", decompressedData);
</script>

</body>
</html>

