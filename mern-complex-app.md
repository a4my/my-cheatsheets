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

Install express and import it to your app.js file as below:

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

## Creating a router

A router has the responsability of listing out urls or routes you want to listen for and then to say what happens for each of this routes.

• Create a new file called router.js

• Import Express for this file too and list out the home page template:

```js
    const express = require('express')
    const router = express.Router()

    router.get('/', function(req, res) {
        res.render('home-guest')
    })

    module.exports = router
```

❗ Now that we've set up a router, the following lines of code in your app.js file...

```js
    app.get('/', function(req,res) {
        res.send("Welcome to our app")
    })
```
...needs to be replaced by the following code since it's already in your router.js file...

```js
    app.use('/', router)
```

...so your app.js now looks like this:

```js
    const express = require('express')
    const app = express()

    const router = require('./router')

    app.use(express.static('public'))
    app.set('views', 'views')
    app.set('view engine', 'ejs')

    app.use('/', router)

    app.listen(3000)
```