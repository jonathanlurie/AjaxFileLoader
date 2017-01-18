# AjaxFileLoader

*This is a work in progress.*

AjaxFileLoader is a ES6 class with only static functions to load files thru AJAX request (aka. XMLHttpRequest). For the moment, regular text files, gunziped text files and raw binary files are covered.

Since AJAX requests are asynchronous, callbacks are called with the loaded data in arguments. A (possibly large) `String` for the text or compressed text files, and an `ArrayBuffer` for binary files.

## Context
Most [3D mesh files](https://github.com/jonathanlurie/mniobjReader) we are working with at [MCIN](http://mcin-cnim.ca/) are descriptive text files, and some of them are huge. When those files are loaded from a server, expecting a user to wait so that a 20MB text chunk gets loaded can be a lost cause. This very small packed lib is an attempt to make that aspect better.

## Examples
See the `index.html` file. Otherwise, here is how it works:

**For a regular text file:**  
```js
// loading an uncompressed text file
AjaxFileLoader.loadTextFile(
  // file URL
  "data/uncompressedfile.txt",

  // success callback
  function(data){
    // ...
    // do something with data, the text content
    // ...
  },

  // error callback
  function(error){
    console.log(error);
  }
)
```

**For a compressed (gz) text file:**  
```js
// loading a compressed (gz, not tar.gz !) text file
AjaxFileLoader.loadCompressedTextFile(
  // file URL
  "data/compressedfile.txt.gz",

  // success callback
  function(data){
    // ...
    // do something with data, the text content of the compressed file
    // ...
  },

  // error callback
  function(error){
    console.log(error);
  }
)
```

**For a binary file:**  
```js
// loading a compressed (gz, not tar.gz !) text file
AjaxFileLoader.loadBinaryFile(
  // file URL
  "data/somebinaryfile_full8_400um_optbal.mnc",

  // success callback
  function(data){

    if(data){
      // ...
      // do something with raw binary data,
      // you could start by getting its size:
      // data.byteLength
      // ...
    }
  },

  // error callback
  function(error){
    console.log(error);
  }
)
```

The file given in example is a minc file, you can open in JS with [MincReaderJS](https://github.com/jonathanlurie/MincReaderJS).


## Dependencies
The high speed zlib port to javascript [Pako](https://github.com/nodeca/pako) is used for the `loadCompressedTextFile`.

## License
MIT
