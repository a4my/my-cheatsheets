---
title: MERN
category: MERN with complex apps
updated: 2021-07-27
intro: |
  A closer look to NPM / Express / Mongo DB / MVC concept (Model View Controller)
---
```
❗❗ Please note this lesson is about using the MERN stack to build a more complex app than building a simple todo app. Here we are building a small social media app. Our app will let you have several users registering and logging in. Posting (crud), following users, liking posts, and a live chat are features that are available in our app.
```

## Setting up our server with Express

Install express and import it to your app.js file as below:

```js
    const express = require('express') // to import Express
    const app = express() // to use Express

    app.use(express.urlencoded({extended: false}))
    app.use(express.json())
    // These 2 lines are mandatory and non-educational. They are only there to let Express accept the 2 common ways of receiving data, the traditional HTML form submit and sending over a bit of json data

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

## Setting up a controller

Controllers allow your router to only list your routes without including the function blocks. Instead, controllers contains all our functions in separate files which the router can call instead of storing them. This is method is for code efficiency and organization purposes.

### First controller's function

• Create a 'controllers' folder and add new files called 'userController.js'.

• Create your first function called 'home' which will render the home-page of our app:

```js
    exports.home = function(req, res) {
    res.render('home-guest')
}
```

• Now that the function 'home' is listed in the userController.js file, the router.js file can call it this way:

```js
    router.get('/', userController.home)
```

• This method is much cleaner than the original code:

```js
    router.get('/', function(req, res) {
        res.render('home-guest')
    })
```

### second example

Let's try to create a function that render the page which should be render when we click on the 'register' button of our home page.

• Make sure the <form> of our home page's html contains an attribute called 'action' and set it up to '/register'.

• Create the function that renders the register landing page in our userController.js file:

```js
    exports.register = function(req, res) {
    res.send("Thanks for trying to register")
} 
```

• Finally, call the 'register' function in our router.js file:

```js
    router.post('/register', userController.register)
```


## Setting up a DOTENV for password protection

• Install the dotenv and mongodb package then crearte a db.js file.

```js
    const dotenv = require('dotenv')
    dotenv.config()

    const MongoClient = require('mongodb').MongoClient

    MongoClient.connect(process.env.CONNECTIONSTRING, {useNewUrlParser: true, useUnifiedTopology: true}, function(err, client) {
        module.exports = client.db()
        const app = require('./app')
        app.listen(process.env.PORT)
    })
```

• Instead of creating a variable called connectionString with our username and password string from MongoDB, we can create a file called '.env' and write the following codes in it:

```
CONNECTIONSTRING=mongodb+srv://todoAppUser:Fender666@cluster0.wlxbg.mongodb.net/ComplexApp?retryWrites=true&w=majority
PORT=3000
```

• Include the .env file onto your .gitignore file so you don't push it onto Github

• You can then replace the connectionString by `process.env.CONNECTIONSTRING` and replace 3000 by `PORT` in your code connecting MongoDB to your app.


## Hashing User Passwords

• `npm install bcryptjs`
• import bcryptjs into your User.js file
• In your register function add the following code:

```js
    let salt = bcrypt.genSaltSync(10)
    this.data.password = bcrypt.hashSync(this.data.password, salt)
```

• In your login function make sure to add the following code so you can log in to your app and match the hashed password:

```js
    if (attemptedUser && bcrypt.compareSync(this.data.password, attemptedUser.password)) {
            resolve("Congrats!")
        }
```

