---
title: NodeJs Modules
category: JavaScript
updated: 2021-09-27
intro: |
  A closer look at NodeJS
---

# Fundamentals of NodeJs

## basic commands in their terminal

```
    node -v // returns the version of node installed on your computer
    node // enters JS mode in the terminal
    ctr+D // will stop the JS mode
    node script.js // will read the JS script

    3*8 = 24
    _+ 6 = 30
    the underscore represents the previous sum


```

## Read & Write files in NodeJS

• create a JS file and use the commands of the FS package:

```js
const fs = require("fs")

const textIn = fs.readFileSync("./txt/input.txt", "utf-8") // To read the input.txt file
console.log(textIn)

const textOut = `This is what we know about the avocado: ${textIn}. \n Created on ${Date.now()}`
fs.writeFileSync("./txt/output.txt", textOut) // To write/create a file called output.txt
console.log("File written")
```

• To activate the script, you must call the following command in the terminal:

`node index.js`

## Read & Write files asynchronously

• Use the asynchronous properties of FS package:

```js
fs.readFile("./txt/start.txt", "utf-8", (err, data1) => {
  fs.readFile(`./txt/${data1}.txt`, "utf-8", (err, data2) => {
    console.log(data2)
    fs.readFile(`./txt/append.txt`, "utf-8", (err, data3) => {
      console.log(data3)

      fs.writeFile("./txt/final.txt", `${data2}\n${data3}`, "utf-8", err => {
        console.log("Your file has been written 😎")
      })
    })
  })
})
console.log("Will read file!")
```

✔😉 Note that the synchronous properties of FS were called `readFileSync` and `writeFileSync` and that the asynchronous ones were called `readFile` and `writeFile`.

## Creating a simple web server

• Import the http package

```js
const http = require("http")
```

• Create a server that listens to request

```js
const server = http.createServer((req, res) => {
  console.log(req)
  res.end("Hello from the server! ✌")
})

server.listen(8000, "127.0.0.1", () => {
  console.log("Listening to request on port 8000")
})
```

• run `node index.js` and open your localhost:8000

## Routing

• Import the url package

```js
const url = require("url")
```

• Using the simple web server we previously created, now use the url package and create an if/else statement to create your routes:

```js
const server = http.createServer((req, res) => {
  const pathName = req.url

  if (pathName === "/" || pathName === "/overview") {
    res.end("This is the OVERVIEW!")
  } else if (pathName === "/product") {
    res.end("This is the PRODUCT")
  } else {
    res.writeHead(404, {
      "Content-type": "text/html",
      "my-own-header": "hello-world"
    })
    res.end("<h1>Page not found</h1>")
  }
})

server.listen(8000, "127.0.0.1", () => {
  console.log("Listening to request on port 8000")
})
```
