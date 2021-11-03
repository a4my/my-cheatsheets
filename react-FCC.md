---
title: REACT
category: REACT Basics
updated: 2021-11-01
intro: |
  Basics of React by FreeCodeCamp.com
---

# Basics of React

### JSX

React is an Open Source view library created and maintained by Facebook. It's a great tool to render the User Interface (UI) of modern web applications.

React uses a syntax extension of JavaScript called JSX that allows you to write HTML directly within JavaScript. However, because JSX is not valid JavaScript, JSX code must be compiled into JavaScript. The transpiler Babel is a popular tool for this process.

❗ One important thing to know about nested JSX is that it must return a single element.

```js
ReactDOM.render(JSX, document.getElementById('root'))

const JSX = (
  <div>
    <p>Paragraph One</p>
    <p>Paragraph Two</p>
    <p>Paragraph Three</p>
  </div>
)
```

### Comments in JSX

To put comments inside JSX, you use the syntax {/\* \*/} to wrap around the comment text.

```js
const JSX = (
  <div>
    <h1>This is a block of JSX</h1>
    {/* This is my comment*/}
    <p>Here's a subtitle</p>
  </div>
)
```

### Render HTML Elements to the DOM

ReactDOM offers a simple method to render React elements to the DOM which looks like this:

```js
ReactDOM.render(componentToRender, targetNode)
```

As you would expect, ReactDOM.render() must be called after the JSX element declarations, just like how you must declare variables before using them.

```js
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
)

const challengeNode = document.getElementById('challenge-node')
ReactDOM.render(JSX, challengeNode)
```

### Define an HTML Class in JSX

One key difference in JSX is that you can no longer use the word `class` to define HTML classes. This is because class is a reserved word in JavaScript. Instead, JSX uses `className`.

In fact, the naming convention for all HTML attributes and event references in JSX become camelCase. For example, a click event in JSX is `onClick`, instead of `onclick`. Likewise, `onchange` becomes `onChange`. While this is a subtle difference, it is an important one to keep in mind moving forward.

```js
const JSX = (
  <div className="my-div">
    <h1>Add a class to this div</h1>
  </div>
)
```

### Self-clsing tags

In JSX, the rules are a little different. Any JSX element can be written with a self-closing tag, and every element must be closed.

The line-break tag, for example, must always be written as <br /> in order to be valid JSX that can be transpiled. A <div>, on the other hand, can be written as <div /> or <div></div>. The difference is that in the first syntax version there is no way to include anything in the <div />.

# React components

### Create a Stateless Functional Component

There are two ways to create a React component. The first way is to use a JavaScript function. Defining a component in this way creates a stateless functional component. cThere are two ways to create a React component. The first way is to use a JavaScript function. Defining a component in this way creates a stateless functional component.

To create a component with a function, you simply write a JavaScript function that returns either JSX or null.

❗ One important thing to note is that React requires your function name to begin with a capital letter.c

```js
const DemoComponent = function () {
  return <div className="customClass" />
}
```

Because a JSX component represents HTML, you could put several components together to create a more complex HTML page. This is one of the key advantages of the component architecture React provides. It allows you to compose your UI from many separate, isolated components. This makes it easier to build and maintain complex user interfaces.

### Create a React Component

The other way to define a React component is with the ES6 class syntax. In the following example, Kitten extends React.Component:

```js
class Kitten extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    return <h1>Hi</h1>
  }
}
```

This creates an ES6 class Kitten which extends the React.Component class. So the Kitten class now has access to many useful React features, such as local state and lifecycle hooks.

Notice the Kitten class has a constructor defined within it that calls super(). It uses super() to call the constructor of the parent class, in this case React.Component. The constructor is a special method used during the initialization of objects that are created with the class keyword.

It is best practice to call a component's constructor with super, and pass props to both. This makes sure the component is initialized properly.

### Create a Component with Composition

Now we will look at how we can compose multiple React components together. Imagine you are building an app and have created three components: a Navbar, Dashboard, and Footer.

To compose these components together, you could create an App parent component which renders each of these three components as children. To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX. For example, in the render method you could write:

```js
return (
  <App>
    <Navbar />
    <Dashboard />
    <Footer />
  </App>
)
```

When React encounters a custom HTML tag that references another component (a component name wrapped in < /> like in this example), it renders the markup for that component in the location of the tag. This should illustrate the parent/child relationship between the App component and the Navbar, Dashboard, and Footer.

```js
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  )
}

class ParentComponent extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        <ChildComponent />
      </div>
    )
  }
}
```

### Use React to Render Nested Components

There are many other different ways you can compose components with React.

Component composition is one of React's powerful features. When you work with React, it is important to start thinking about your user interface in terms of components like the App example in above. You break down your UI into its basic building blocks, and those pieces become the components. This helps to separate the code responsible for the UI from the code responsible for handling your application logic. It can greatly simplify the development and maintenance of complex projects.

```js
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
        <li>Strawberries</li>
        <li>Bananas</li>
      </ul>
    </div>
  )
}

const Fruits = () => {
  return (
    <div>
      <TypesOfFruit />
    </div>
  )
}

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
      </div>
    )
  }
}
```

### Compose React components

Rendering ES6 style class components within other components is no different than rendering the simple components you used above. You can render JSX elements, stateless functional components, and ES6 class components within other components.

```js
class Fruits extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div>
        <h2>Fruits:</h2>
        <NonCitrus />
        <Citrus />
      </div>
    )
  }
}

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
        <Vegetables />
      </div>
    )
  }
}
```

### Render a Class Component to the DOM

React components are passed into `ReactDOM.render()` a little differently than JSX elements. For JSX elements, you pass in the name of the element that you want to render. However, for React components, you need to use the same syntax as if you were rendering a nested component, for example `ReactDOM.render(<ComponentToRender />, targetNode)`. You use this syntax for both ES6 class components and functional components.

```js
class TypesOfFood extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
        <Vegetables />
      </div>
    )
  }
}

const targetNode = document.getElementById('challenge-node')
ReactDOM.render(<TypesOfFood />, targetNode)
```

# Props

### Pass Props to a Stateless Functional Component

In React, you can pass `props`, or properties, to child components. Say you have an App component which renders a child component called Welcome which is a stateless functional component. You can pass `Welcome` a `user` property by writing:

```js
<App>
  <Welcome user="Mark" />
</App>
```

You use `custom HTML attributes` created by you and supported by React to be passed to the component. In this case, the created property user is passed to the component Welcome. Since Welcome is a stateless functional component, it has access to this value like so:

```js
const Welcome = props => <h1>Hello, {props.user}!</h1>
```

It is standard to call this value props and when dealing with stateless functional components, you basically consider it as an argument to a function which returns JSX. You can access the value of the argument in the function body. With class components, you will see this is a little different.

```js
const CurrentDate = props => {
  return (
    <div>
      <p>The current date is: {props.date}</p>
    </div>
  )
}

class Calendar extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        <CurrentDate date={Date()} />
      </div>
    )
  }
}
```

### Pass an Array as Props

To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.

```js
<ParentComponent>
  <ChildComponent colors={['green', 'blue', 'red']} />
</ParentComponent>
```

The child component then has access to the array property colors. Array methods such as `join()` can be used when accessing the property. `const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>` This will join all colors array items into a comma separated string and produce: `<p>green, blue, red</p>`

```js
const List = props => {
  return <p>{props.tasks.join(', ')}</p>
}

class ToDo extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        <List tasks={['walk dog', 'workout']} />
        <h2>Tomorrow</h2>
        <List tasks={['walk dog', 'workout', 'eat']} />
      </div>
    )
  }
}
```

### Use Default Props

React also has an option to set default props. You can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. This allows you to specify what a prop value should be if no value is explicitly provided. For example, if you declare `MyComponent.defaultProps = { location: 'San Francisco' }`, you have defined a location prop that's set to the string `San Francisco`, unless you specify otherwise. React assigns default props if props are undefined, but if you pass `null` as the value for a prop, it will remain `null`.

```js
const ShoppingCart = props => {
  return (
    <div>
      <h1>Shopping Cart Component</h1>
    </div>
  )
}
// Change code below this line

ShoppingCart.defaultProps = { items: 0 }
```

### Override Default Props

The ability to set default props is a useful feature in React. The way to override the default props is to explicitly set the prop values for a component.

```js
const Items = props => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return <Items quantity={100} />
  }
}
```
