---
toc: false
comments: false
layout: post
title: Data Compression
description: :D
type: ccc
courses: { csp: {week: 13} }
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Run-Length Encoding (RLE) Compression</title>
</head>
<body>
<input type='file' onchange="readFile(this);" />
<script>
  function toBinary(input, callback) {
    if (typeof input === 'string') {
      // If input is a URL
      var xhr = new XMLHttpRequest();
      xhr.onload = function() {
        var reader = new FileReader();
        reader.onloadend = function() {
          // Convert binary string to ArrayBuffer
          var binaryData = new Uint8Array(Array.from(reader.result)).buffer;
          callback(binaryData);
        };
        xhr.open('GET', input);
        xhr.responseType = 'arraybuffer';
        xhr.send();
      };
    } else if (input instanceof File) {
      // If input is a File
      var reader = new FileReader();
      reader.onloadend = function() {
        // Convert binary string to ArrayBuffer
        var binaryData = new Uint8Array(Array.from(reader.result)).buffer;
        callback(binaryData);
      };
      reader.readAsArrayBuffer(input);
    }
  }

  function readFile(inputElement) {
    var file = inputElement.files[0];
    if (file) {
      toBinary(file, function(binaryData) {
        console.log('File as Binary Data:', binaryData);
        // Use binaryData as the original data
        let originalData = binaryData;
        let compressedData = compress(originalData);
        console.log("Original data:", originalData);
        console.log("Compressed data:", compressedData);
      });
    }
  }

  function compress(inputData) {
    let compressedData = "";
    let count = 1;

    // Convert binary data to array of integers
    let inputArray = new Uint8Array(inputData);

    // Iterate through the input array
    for (let i = 1; i < inputArray.length; i++) {
      if (inputArray[i] === inputArray[i - 1]) {
        count++;
      } else {
        compressedData += inputArray[i - 1] + count + ",";
        count = 1;
      }
    }

    // Add the last element and its count
    compressedData += inputArray.slice(-1)[0] + count;
    return compressedData;
  }
</script>
</body>
</html>
