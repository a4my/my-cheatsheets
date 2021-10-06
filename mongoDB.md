---
title: Mongo DB
category: MERN Basics
updated: 2021-10-04
intro: |
  A closer look to Mongo DB
---

❗❗ Warning: These notes are based on the MERN lessons with Jonas Schmedtan. Full code at the end of these notes.

# Setting up MongoDB Compass

Download MongoDB Compass from the website and download the server version for desktop.

Once installed, create on your `C:/This PC` a `data` folder ith a `db` subfolder.

Go back up to `C:/Program Files/MongoDB/Server/5.0/bin` in your command line or Windows Powershell and open the MongoDb server by running `mongod.exe`

💢 Note that the `b` of MongoDB is actually missing in the command to run❗

In order to launch the server, open a second window in your command line and run `mongo` while the server is listening on your first window.

# Creating a Local Database

• To create a new database, run `use <name-of-collection>` ie (use natours-test)

• The server will switch to the newly created database and return `switched to db <name-of-collection>`

• To insert a document in the database's collection, run `db.tours.insertOne({name: "The Forest Hiker", price: 297, rating: 4.7})`.

> > This will insert a new document and create in the same time a new collection called `tours` in this example. The new document is a JSON object.

💥Note that every document needs to be inserted into a collection!
💥Note that JSON only accepts `double quotes` no single quotes.

### Extra useful commands

• To read the newly created document from the terminal, run `db.tours.find()`

• Run `show dbs` to see all your databases

• Run `shows collections` to see all the collections of a database

• Use `quit()` to quit the mongo shell.

# Creating documents

• Use `db.<collection-name>.insertMany()` to insert a new document into the database's collection. You can insert a JSON object like the example below:

```js
db.tours.insertMany([
  { name: 'The Sea Explorer', price: 497, rating: 4.8 },
  { name: 'The Snow Adventurer', price: 997, ratings: 4.9, difficulty: 'easy' }
])
```

> > Run `db.<collection-name>.find()` to show the collection.

# Querying (reading) documents

• To filter your search in the database, `db.<collection-name>.find({ <property> : <value> })`

For example: db.tours.find({ name : "The Snow Adventurer"})

> > Only the document containing the filter will be read

❗ Note that you still need to use {} when you filter an object

• You can also filter using criterias:

`db.tours.find({ price: {$lte: 500} })`

> > This will return every tours in the database that costs less than or equal to £500.

`db.tours.find({ price: {$lt: 500}, ratings: {$gte: 4.8} })`

> > This will return every tours in the database that strictly cost less than £500 AND for which the ratings is greater than or equal to 4.8.

`db.tours.find({ $or: [{price: {$lt: 500}}, rating: {$gte: 4.8}]})`

> > This will filter your search filtering with one condition OR the other one.

• Add `{name: 1}` to your search to only return the name criteria of the object:

`db.tours.find({ $or: [{price: {$lt: 500}}, rating: {$gte: 4.8}]}, { name: 1 })`

> > "\_id" : ObjectId("615af0c9c33afc263051b06e"), "name" : "The Sea Explorer"

# Updating documents

• Run `db.<collection-name>.updateOne({ name: <name>}, {$set: {property; <new-value>}})` to update a document:

```js
db.tours.updateOne({ name: 'The Snow Adventurer' }, { $set: { price: 597 } })
```

This command will return the following response:

```js
    { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

And if you check again your database's collection, you'll see that the document has been updated:

```js
    { "_id" : ObjectId("615af0c9c33afc263051b06f"), "name" : "The Snow Adventurer", "price" : 597, "rating" : 4.9, "difficulty" : "easy" }
```

# Deleting documents

• `db.<collection-name>.deleteMany({ })` will delete the whole collection

• `db.<collection-name>.deleteMany({ })` will delete documents that match the filters condition:

```js
db.tours.deleteMany({ rating: { $lt: 4.8 } })
```

> > This will delete any tour that have a rating less than4.8

• `db.<collection-name>.deleteOne({ name: "<name>" })` will delete the document targetted by the name property

# Creating a Hosted Database for your project

• Open MongoDB Atlas
• Click on `New Project`
• Give it a name (<project-app>)
• Click again on `create project` in the permissions window
• Then click on `Build a database`
• Choose the free server option and click on `Create Cluster`

# Connecting your Hosted Database to your project

• On your `clusters` list, click on `connect`
• Choose `Add Your Current IP Address`
• Create a database user by picking up a username and a password
✔ You can already copy and paste your password to the config.env file of your project 😉
• Click on `Create Database User` then on `Choose connection method`

• Click on `Connect using MongoDB Compass` and choose the `I already have MongoDB Compass` option
• Copy the `connection string` and open MongoDB Compass on your desktop.

• If Compass has not detected itself that you have a connection string copied in your clipboard, click on `Connect to` and paste the connection string and add your password inside the string.

> > You will then land on your project's database dashboard

• Click on `Create a database`, choose a name for your database AND a name for your first collection.

• Click on your newly created database then on your newly reated collection and click on `Add data` to insert a new document.

### Connecting your database from anywhere if ou work on a different computer (OPTIONAL)

• Open MongoDB Atlas and on your cluster's list, click on `Network Access`
• Then on `Add IP Address` and choose `Allow Acces From Anywhere `

### Connect the database to your Mongo Shell

• Open MongoDB Atlas and on your cluster's list, click on `Connect`
• Click on `Connect using MongoDB Shell` and choose the `I already have MongoDB Shell` option
• Copy the `connection string` and open MongoDB Compass on your desktop.
