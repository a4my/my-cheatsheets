---
title: Heroku
category: Hosting
updated: 2021-07-26
intro: |
  How to push your app on the internet with Heroku
---

## Linking your Heroku account to your app
Go to heroku.com to download the windows or mac installer. Once installed, run `heroku login` in your command line to log in to your Heroku account via your web browser.

😉 You can run `heroku --version` to check your version of Heroku and if it has been installed correctly.

## Setting up Heroku in your app

• Create a `procfile` file and type down:

```
    web: node server.js
```

• Also add in your server.js file the following lines of code:

```js
    let port = process.env.PORT
    if (port == null || port =='') {
        port = 3000
    }
```

• And make sure you replace

```js
    mongodb.connect(connectionString, {useNewUrlParser: true, useUnifiedTopology: true}, function(err, client) {
        db = client.db()
        app.listen(3000)
}) 
```

with

```js
    mongodb.connect(connectionString, {useNewUrlParser: true, useUnifiedTopology: true}, function(err, client) {
        db = client.db()
        app.listen(port)
}) 
```

## Pushing your app to Heroku

❗ Make sure you include a `.gitignore` file in your project and write down as `nod_modules` to avoid uploading the local node_modules folder.

• Push your project onto Github

• Run the following command to push the app in the command line but not the VS code one

```
    heroku git:remote -a <app name>
```

• Finally, run:

```
    git push heroku master
```

❗❗ Make sure to use the command line from your desktop and not from VS Code as it doesn't seem to work correctly when using the VS Code one.


## Pushing future changes to your Heroku app

In a different command line run:

```
    git status
    git add .
    git commit -m "your message"
    git push heroku master
```