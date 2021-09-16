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
• Add the following script in your Main.js file:

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

• Finally enter your HTML markup inside the return of your function using the JSX syntax (which means some of the html properties needs to be renamed ie class becomes className and autocomplete becomes autoComplete):

```js
import React from "react"
// Note that React DOM doesn't need to be imported like we did in the main script

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

# Routing in React

Now that we have installed and set up React and learn how to create reusable components with React, the next learning stage would be to set up a router to connect differents pages of your app with one another.

## Setting up React Router DOM

• `npm install react-router-dom` to download React Router DOM
• For this particular package the import onto your Main.js file looks slightly different due to the destructuring we need to do with this package:

```js
import { BrowserRouter, Switch, Route } from "react-router-dom"
```

• BrowserRouter, Switch and Route are options that comes from React-Router-DOM and will help up to create routes within our app. These 3 options can be use like "html tags" within our Main function to create routes but also to create paths or keep components in our web browser components that have already been rendered and that won't need to be rendered again.

• Remember our Main function?

```js
function Main() {
  return (
    <>
      <Header />
      <Terms />
      <Footer />
    </>
  )
}
```

• Now React Router DOM let us use the Main function this way to create a router:

```js
function Main() {
  return (
    <BrowserRouter>
      <Header />
      <Switch>
        <Route path="/" exact>
          <HomeGuest />
        </Route>
        <Route path="/about-us" exact>
          <About />
        </Route>
        <Route path="/terms" exact>
          <Terms />
        </Route>
      </Switch>
      <Footer />
    </BrowserRouter>
  )
}
```

• BrowserRouter represents the elements that are going to be rendered from our Main function.

• The Header and Footer "tags" are components that only needs to be rendered once.

• Switch regroups all the different components that are going to be switched to within the same page ie Home, About and Terms links that are at the bottom of the home page

• Finally the route "tags" allow us to provide a URL path to these components ie ourApp/about

## Converting html anchor tags to React links

• If we look at the Footer component, we can see that we used an HTML mark up for the footer.

```js
import React from "react"
import { Link } from "react-router-dom"

function Footer() {
  return (
    <footer className="border-top text-center small text-muted py-3">
      <p>
        <a href="/" className="mx-1">
          Home
        </a>{" "}
        |{" "}
        <a className="mx-1" href="/about-us">
          About Us
        </a>{" "}
        |{" "}
        <a className="mx-1" href="/terms">
          Terms
        </a>
      </p>
      <p className="m-0">
        Copyright &copy; 2020{" "}
        <a href="/" className="text-muted">
          ComplexApp
        </a>
        . All rights reserved.
      </p>
    </footer>
  )
}

export default Footer
```

• However, React does not read HTML anchor tags and uses <Link> tags instead as opposed to <a> in html. So you need to manually swap the React tags so the Router can properly work

• Also the `href` attribute needs to be changed to `to`

# Composiiton & Page title switch

A quick note about composiiotn and page title changing in the web browser when switching to a new link or new page.

We created a Container component earlier that we used as a container div for the content of every page:

```js
import React, { useEffect } from "react"

function Container(props) {
  return <div className={"container py-md-5 " + (props.wide ? "" : "container--narrow")}>{props.children}</div>
}

export default Container
```

And we also replaced the html container div of our pages's content with this new React Container tag:

```js
function About() {
  return (
    <Container>
      <h2>About Us</h2>
      <p class="lead text-muted">Lorem ipsum dolor sit amet consectetur adipisicing elit. Corporis dolorum labore quisquam vel id dicta fuga! Ducimus, quo. Dolore commodi aliquid error veritatis consequuntur, excepturi cumque fuga eum incidunt doloremque?</p>
    </Container>
  )
}
```

In order to make the page title appear on the web browser and change when clicking onto a new link, we need to use composition and make some modifications to our components.

• Firstly, create a Page component and write the following script:

```js
import React, { useEffect } from "react"
import Container from "./Container" // ❗ Note that this new component do need to import the Container component

function Page(props) {
  useEffect(() => {
    document.title = `${props.title} | OurApp` // wiil update the title
    window.scrollTo(0, 0) // will scroll back up when loading the new page
  }, [])

  return <Container wide={props.wide}>{props.children}</Container> // will use the script from the Container component
}

export default Page
```

• Finally, replace in your app components the import of the Container component with the new Page component and replace the <Container> tags with <Page> tags. Do not forget to add a title attribute in the opening <Page> tag:

```js
import React, { useEffect } from "react"
import Page from "./Page" // replaced the old Container component

function About() {
  return (
    <Page title="About Us">
      <h2>About Us</h2>
      <p class="lead text-muted">Lorem ipsum dolor sit amet consectetur adipisicing elit. Corporis dolorum labore quisquam vel id dicta fuga! Ducimus, quo. Dolore commodi aliquid error veritatis consequuntur, excepturi cumque fuga eum incidunt doloremque?</p>
    </Page>
  )
}

export default About
```

Now the page title will change when your navigates between pages.
