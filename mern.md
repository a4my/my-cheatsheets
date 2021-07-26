---
title: MERN
category: MERN
updated: 2021-07-24
intro: |
  A closer look to NPM / Express / Mongo DB / Axios
---

❗❗ Warning: These notes are based on the To-do App lessons with Brad Schiff. Full code at the end of these notes.

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
  let MongoClient = require('mongodb').MongoClient
  let db;

  let connectionString = 'mongodb+srv://todoAppUser:<Fender666>@cluster0.wlxbg.mongodb.net/TodoApp?retryWrites=true&w=majority'
  
  MongoClient.connect(connectionString, {useNewUrlParser: true, useUnifiedTopology: true}, function(err, client) {
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

## Creating and updating an item into the database and on the frontend

• Creating an item:

```js
app.post('/create-item', function(req, res) {
    db.collection('items').insertOne({text: req.body.item}, function() {
        res.redirect('/')
    })
})

```

• Updating an item:

```js
app.post('/update-item', function(req, res) {
    db.collection('items').findOneAndUpdate({_id: new ObjectId(req.body.id)}, {$set: {text: req.body.text}}, function() {
        res.send("Success")
    })
})
```

also add the following in your browser.js file:

```js
  document.addEventListener('click', function(e){
    if(e.target.classList.contains('edit-me')) {
        let userInput = prompt("Enter you desired new text", e.target.parentElement.parentElement.querySelector(".item-text").innerHTML)
        if(userInput) {
            axios.post('/update-item', {text: userInput, id: e.target.getAttribute("data-id")}).then(function() {
                e.target.parentElement.parentElement.querySelector(".item-text").innerHTML = userInput
                 
            }).catch(function() {
                console.log("Please try again later.")
            })
        }
    }
})
```

The above line of codes will allow you to edit an item of your to-do list when clicking on its edit button. The item will also appears in the prompt window's input.


## Deleting an item from the database and the frontend

```js
  document.addEventListener('click', function(e){
    //Delete feature
    if(e.target.classList.contains('delete-me')) {
        if(confirm("Do you really want to delete this item permanently?")) {
            axios.post('/delete-item', {id: e.target.getAttribute("data-id")}).then(function() {
                e.target.parentElement.parentElement.remove()
            }).catch(function() {
                console.log("Please try again later.")
            })
        }
    }

    // Update feature
    if(e.target.classList.contains('edit-me')) {
        let userInput = prompt("Enter you desired new text", e.target.parentElement.parentElement.querySelector(".item-text").innerHTML)
        if(userInput) {
            axios.post('/update-item', {text: userInput, id: e.target.getAttribute("data-id")}).then(function() {
                e.target.parentElement.parentElement.querySelector(".item-text").innerHTML = userInput  
            }).catch(function() {
                console.log("Please try again later.")
            })
        }
    }
})
```

and add the following line of codes so axios can communicate with MongoDB and remove the item from the database:

```js
  app.post('/delete-item', function(req, res){
    db.collection('items').deleteOne({_id: new ObjectId(req.body.id)}, function() {
        res.send("Success")
    })
})
```

## Creating a new item without a page reload

```js
  function itemTemplate(item) {
    return `<li class="list-group-item list-group-item-action d-flex align-items-center justify-content-between">
    <span class="item-text">${item.text}</span>
    <div>
    <button data-id="${item._id}" class="edit-me btn btn-secondary btn-sm mr-1">Edit</button>
    <button data-id="${item._id}" class="delete-me btn btn-danger btn-sm">Delete</button>
    </div>
    </li>`
  }
  
  // Create Feature
  let createField = document.getElementById("create-field")
  
  document.getElementById("create-form").addEventListener("submit", function(e) {
    e.preventDefault()
    axios.post('/create-item', {text: createField.value}).then(function (response) {
      // Create the HTML for a new item
      document.getElementById("item-list").insertAdjacentHTML("beforeend", itemTemplate(response.data))
      createField.value = ""
      createField.focus()
    }).catch(function() {
      console.log("Please try again later.")
    })
  })
```

and add onto your server.js file to update the database:

```js
  app.post('/create-item', function(req, res) {
    db.collection('items').insertOne({text: req.body.text}, function(err, info) {
        if(err) {         
            console.log('Error occurred while inserting');     
        } 
        else {        
        let data = {          
            "_id": info.insertedId,          
            "text": req.body.text        
        }       
         res.json(data);  
    }})
  })
```

## Client side rendering

Initial page load rendering:

• in your browser.js file, add the following code:

```js
// Initial page load rendering
let ourHTML = items.map(function(item) {
    return itemTemplate(item)
}).join('')
document.getElementById('item-list').insertAdjacentHTML('beforeend', ourHTML)
```

• also add a new script at the bottom of your server.js file:

```js
<script>
  let items = ${JSON.stringify(items)}
</script>
```

• Make sure you remove the li element from the HTML in your server.js since it will now be generated by the itemTemplate() function