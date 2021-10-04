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

• The server will switch to the newly created dataase and return `switched to db <name-of-collection>`

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

> > Run `db.<collection-name>.find()` to show the coolection.

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
