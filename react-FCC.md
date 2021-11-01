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
