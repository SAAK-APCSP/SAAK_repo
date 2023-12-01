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
          // Convert binary string to Uint8Array
          var binaryData = new Uint8Array(reader.result);
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
        // Convert binary string to Uint8Array
        var binaryData = new Uint8Array(reader.result);
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
        let compressedData = compress(binaryData);
        console.log("Compressed data:", compressedData);
      });
    }
  }
  function compress(inputData) {
    let compressedData = "";
    let count = 1;
    // Iterate through the input array
    for (let i = 1; i < inputData.length; i++) {
      if (inputData[i] === inputData[i - 1]) {
        count++;
      } else {
        compressedData += String(count) + inputData[i - 1] + ",";
        count = 1;
      }
    }
    // Add the last element and its count
    compressedData += inputData[inputData.length - 1] + count;
    return compressedData;
  }
</script>
</body>
</html>
