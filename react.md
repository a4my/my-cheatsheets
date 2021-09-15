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

# Creating reusable components

## Component JS file

• Create a `component` folder in your app
• Create a file for your component ie `Header.js` (it's industry standard to capitalize the name of the component file)
• Start your script with `3 mandatory elements`: importing react, your function and exporting component:

```js
    import React from "react"

    function Header() {
    return (

    )
    }

    export default Header

    //This is the boilerplate of every React component
```

• Finally enter your HTML markup inside the return of your function using the JSX syntax (which means some of the html classes needs to be renamedie class becomes className and autocomplete becomes autoComplete):

```js
import React from "react"

function Header() {
  return (
    <header className="header-bar bg-primary mb-3">
      <div className="container d-flex flex-column flex-md-row align-items-center p-3">
        <h4 className="my-0 mr-md-auto font-weight-normal">
          <a href="/" className="text-white">
            {" "}
            ComplexApp{" "}
          </a>
        </h4>
        <form className="mb-0 pt-2 pt-md-0">
          <div className="row align-items-center">
            <div className="col-md mr-0 pr-md-0 mb-3 mb-md-0">
              <input name="username" className="form-control form-control-sm input-dark" type="text" placeholder="Username" autoComplete="off" />
            </div>
            <div className="col-md mr-0 pr-md-0 mb-3 mb-md-0">
              <input name="password" className="form-control form-control-sm input-dark" type="password" placeholder="Password" />
            </div>
            <div className="col-md-auto">
              <button className="btn btn-success btn-sm">Sign In</button>
            </div>
          </div>
        </form>
      </div>
    </header>
  )
}

export default Header
```

## Using your component in your app

• So far, this is how your Main.js file looks like:

```js
    import React from "React"
    import ReactDOM from "react-dom"

    function Main() {
    return ()
    }

    ReactDOM.render(<Main />, document.querySelector("#app"))

    if (module.hot) {
    module.hot.accept()
    }
```

• The 2 imports tells your Main.js file to use React and ReactDOM
• The function called Main is what we are going to tell ReactDOM to render (ie html template components, etc)
• The ReactDOM.render() function tells ReactDOM which function to render and where in the HTML markup (in this example in the div with the id of 'app')

• To start using your React components, you need to import them onto your Main.js file:

```js
import Header from "./components/Header"
import HomeGuest from "./components/HomeGuest"
import Footer from "./components/Footer"
```

• Finally you must tell your function Main to use them and render them:

```js
function Main() {
  return (
    <>
      <Header />
      <HomeGuest />
      <Footer />
    </>
  )
}
```

• Your Main.js file should like this now:

```js
import React from "React"
import ReactDOM from "react-dom"

// Components
import Header from "./components/Header"
import HomeGuest from "./components/HomeGuest"
import Footer from "./components/Footer"

function Main() {
  return (
    <>
      <Header />
      <HomeGuest />
      <Footer />
    </>
  )
}

ReactDOM.render(<Main />, document.querySelector("#app"))

if (module.hot) {
  module.hot.accept()
}
```
