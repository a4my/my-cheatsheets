---
title: REACT
category: REACT Basics
updated: 2021-09-15
intro: |
  A closer look to React
---

# Basics of React

## Setting up React

`npm init -y` to create a package.json file
`npm install react react-dom` to download React and React-dom, this command will also create a package-lock.json file and download the node_modules folder

## Example of a small React App

• Created an HTML file with an id div of `app`
• Created a Main.js file and `make sure the language mode in VS code is Javascript React`
• Add the following script in youor Main.js file:

```js
import React from "React"
import ReactDOM from "react-dom"

function ExampleComponent() {
  return (
    <div>
      <h1>This is our app!</h1>
      <p>The sky is blue</p>
    </div>
  )
}

ReactDOM.render(<ExampleComponent />, document.querySelector("#app"))
```

❗❗❗❗❗❗ The small app above won't work in web browsers at this stage and a bundler that compiles all the files above is needed. This is why we use WebPack.

## Installing WebPack

• `npm i webpack webpack-cli webpack-dev-server` to download 3 packages that we need to use Webpack

• Create a webpack file in your main app called `webpack.config.js`

• `npm i @babel/core @babel/preset-env @babel/preset-react babel-loader` to download 4 packages which will help us using Webpack with Babel

• Back into our `webpack.config.js`file make sure to save the following settup script for Webpack and Babel:

```js
const path = require("path")

module.exports = {
  entry: "./app/Main.js",
  output: {
    publicPath: "/",
    path: path.resolve(__dirname, "app"),
    filename: "bundled.js"
  },
  mode: "development",
  devtool: "source-map",
  devServer: {
    port: 3000,
    static: path.join(__dirname, "app"),
    hot: true,
    historyApiFallback: { index: "index.html" }
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /(node_modules)/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-react", ["@babel/preset-env", { targets: { node: "12" } }]]
          }
        }
      }
    ]
  }
}
```

❗❗❗ Make sure you change the script source of your html file to `/bundled.js` to link the final script that Webpack and Babel will be creating for the web browsers to read our files.

• In our `package.json` file, create the following script:

```js
    "dev": "webpack serve"
```

• In your command line, run `npm run dev`and open your localhost:3000 in your web browswer to see your app.

❕ Do add the following script at the bottom of your Main.js file so the Javascript of your React app is saved and rendered asynchronously :

```js
if (module.hot) {
  module.hot.accept()
}
```

✔ Note that the bundled.js does not appear in your files, this is because webpack keep it in memory and doesn't bother showing it to us until the final stage of bundling our app for deployment.
