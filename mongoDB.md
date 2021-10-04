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
