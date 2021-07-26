---
title: MERN
category: MERN
updated: 2021-07-24
intro: |
  A closer look to NPM / Express / Mongo DB
---

## Top NPM commands

* `npm init` - displays a simple wizard to help you create and define your new project
* `npm install module_name`: install a module;
* `npm install -g module_name`: install a global module;
* `npm install module_name --save`: install a module and add it into the `package.json` file, inside dependencies;
* `npm install module_name --save-dev` - install a module and add it into the `package.json` file, inside devDependencies;
* `npm list` - lists all the modules installed on the project;
* `npm list -g` - lists all the installed global modules
* `npm remove module_name` - uninstall a module from the project;
* `npm remove -g module_name` - uninstall a global module;
* `npm remove module_name --save` - uninstall a module from the project and also remove it from the attribute dependencies
* `npm remove module_name --save-dev` - uninstall a module from the project and also remove it from the attribute devDependencies;
* `npm update module_name` - updates the module version
* `npm update -g module_name` - updates the a global module version
* `npm -v` - displays the npm current version;
* `npm adduser username` - creates an account to npmjs.org2;
* `npm whoami` - displays details of your public npm’s profile (you must create an account using the previous command;
* `npm publish` - publishes a module into npmjs.org (it’s necessary to have an active account first);

## Setting up Express

`npm init -y` to create a package.json file
`npm install express` to download Express
`node app` to run our script called app

in our script called app.js:
```js
    let express = require('express') // will link to express
    let app = express() // will finally call express

    app.use(express.urlencoded({extended: false})) // Mandatory boilerplate, tells express to add all forms values to a body object and add the body object to the req object, by default Express doesn't do it automatically
    
    app.get('/', function(req,res) {
        res.send("Welcome to our new app")
    })

    app.listen(3000) // will use the 3000 local host to run our app
```

`npm install ejs` to download ejs
`npm install nodemon` to download nodemon which automatically refreshes the page localhost

add `"watch": "nodemon app"` in the package.json and run `npm run watch` so nodemon watches for changes


## Connecting Express to Mongo DB

`npm install mongodb` to download Mongo DB

```js
  let mongodb = require('mongodb')
  let db;

  let connectionString = 'mongodb+srv://todoAppUser:<Fender666>@cluster0.wlxbg.mongodb.net/TodoApp?retryWrites=true&w=majority'
  
  mongodb.connect(connectionString, {useNewUrlParser: true, useUnifiedTopology: true}, function(err, client) {
      db = client.db()
      app.listen(3000)
  })
```

```
  Create a new database on MongoDB, click on 'connect', choose a 'different IP address' and enter 0.0.0.0/0, then click on 'Connect your application', create a username and a password for your application access, you will get the following:

  mongodb+srv://todoAppUser:<password>@cluster0.wlxbg.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
```
❗ Make sure to enter your actual password between the <> and add the name of the database on mongo DB instead of 'myFristDatabase' in the link above when copying and pasting it in your script in 'connectionString'

## Linking different scripts to your app

Let's say you have a server.js script to which you would like to link another script called browser.js.

Create a sub-folder called 'public'in your app to include the browser.js file and add the following line of code to let Express have access to the sub-folder and use the script:

```js
  app.use(express.static('public'))
```

## Sending data to your server using Axios

Get the CDN link at https://github.com/axios/axios and paste it onto your server.js file:

```js
              <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

Also add, the following line to your server.js script: 

```js
  app.use(express.json())
```

This line tells Express to automatically take submitted form data and add it to a body object that lives on a request object for asynchronous request
