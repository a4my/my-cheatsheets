---
title: MERN
category: MERN with complex apps
updated: 2021-07-27
intro: |
  A closer look to NPM / Express / Mongo DB / 
---
```
❗❗ Please note this lesson is about using the MERN stack to build a more complex app than building a simple todo app. Here we are building a small social media app. Our app will let you have several users registering and logging in. Posting (crud), following users, liking posts, and a live chat are features that are available in our app.
```

## Setting up our server with Express

• install express and import it to your app.js file as below:

```js
    const express = require('express') // to import Express
    const app = express() // to use Express

    app.use(express.static('public')) // to let Express know to use the 'public' folder for extra css 
    app.set('views', 'views') // to set the views (or templates) configuration and point it to our 'views' folder.
    app.set('view engine', 'ejs') // to tell Express which engine we are using. In this app, our templates we'll be ejs files (ie: home-guest.ejs)

    app.get('/', function(req,res) {
        res.send("Welcome to our app")
    }) // to render our application (here it will only render the message for now)

    app.listen(3000)
```