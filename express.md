---
title: Express
category: MERN Basics
updated: 2021-09-29
intro: |
  A closer look to Express
---

❗❗ Warning: These notes are based on the MERN lessons with Jonas Schmedtan. Full code at the end of these notes.

# Setting up Express

• `npm init -y` to create a package.json file
• `npm install express` to download Express
• create an `app.js` file to call Express and import express to your project:

```js
const express = require('express')
const app = express()
```

• specify the port on which Express is running on:

```js
const port = 3000
app.listen(port, () => {
  console.log(`App running on port ${port}...`)
})
```

### Send your first requests to the server

• test your set up with your first request to the server:

```js
app.get('/', (req, res) => {
  res.status(200).send('Hello from the server side!')
})
```

• `nodemon app.js` to see the server response onto the console
=> you can then open your localhost:3000, or your Postman desktop or Insomnia desktop App to see the response from the server.

You can also pass an object instead of a string by using the .json property:

```js
app.get('/', (req, res) => {
  res
    .status(200)
    .json({ message: 'Hello from the server side!', app: 'Natours' })
})
```

==>

```js
{
  "message": "Hello from the server side!",
  "app": "Natours"
}
```

You can also send a `POST` request to the server:

```js
app.post('/', (req, res) => {
  res.send('You can post to this endpoint...')
})
```

### Handling POST requests in your project

Express does not put the body data on the `req` parameter so we need to add a `middleware`. A middleware is a function that can modify the incoming request data:

```js
app.use(express.json()) // to add below your imports
```

In short the middleware adds the data from the body gets added to the `req` object.

😉 Entire chapter about middlewares coming later.
