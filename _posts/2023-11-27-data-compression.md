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
  function toDataURL(input, callback) {
    if (typeof input === 'string') {
      // If input is a URL
      var xhr = new XMLHttpRequest();
      xhr.onload = function() {
        var reader = new FileReader();
        reader.onloadend = function() {
          callback(reader.result);
        };
        reader.readAsDataURL(xhr.response);
      };
      xhr.open('GET', input);
      xhr.responseType = 'blob';
      xhr.send();
    } else if (input instanceof File) {
      // If input is a File
      var reader = new FileReader();
      reader.onloadend = function() {
        callback(reader.result);
      };
      reader.readAsDataURL(input);
    }
  }
  function readFile(inputElement) {
    var file = inputElement.files[0];
    if (file) {
      toDataURL(file, function(dataUrl) {
        console.log('File to Data URL:', dataUrl);
        // Use dataUrl as the original data
        let originalData = dataUrl.split(',')[1];
        let compressedData = compress(originalData);
        console.log("Original data:", originalData);
        console.log("Compressed data:", compressedData);
      });
    }
  }
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
</script>
</body>
</html>
