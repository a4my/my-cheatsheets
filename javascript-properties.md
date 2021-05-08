---
title: JavaScript Properties
category: JavaScript
updated: 2021-05-03
intro: |
  A random list of properties often used in JS
---

# Properties

## DOM

• Select an element in the HTML:

```js
document.querySelector(".class");
document.querySelectorAll(".class");

document.getElementById("id-name");
```

• Properties to manipulate the HTML element:

```js
document.querySelector(".score").textContent;
document.querySelector(".score").textContent = 13;
document.querySelector(".guess").value;
document.querySelector(".guess").value = 99;
```

## Events

```js
document.querySelector('.class').addEventListener('click', function() {
  // addEventListner has 2 arguments an event and a function
  console.log(document.querySelector('.guess').value;)
  console.log(document.querySelector(".score").textContent = 'Correct Number!';)
})
```
