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

```js
document.addEventListener("keydown", function (e) {
  console.log(e.key); // will return the code for each key pressed down
});
```

## Math Object

The Math object has several properties

```js
const number = Math.random(); // will return a DECIMAL number between 0 and 1
```

If you need a number between 0 and 20 you'll need to multiply by 20

```js
const number = Math.random() * 20; // will return a DECIMAL number between 0 and 20
```

If you need a number without any decimal, use trunc()

```js
const number = Math.trunc(Math.random() * 20) + 1; // will return a number between 0 and 20

❗ // you need to add "+1" otherwise random() will only generate numbers between 0 and 19
```

## Style Manipulation

Changing CSS properties:

```js
document.querySelector("body").style.backgroundColor = "#60b347";
document.querySelector(".number").style.width = "30rem";
```

❗ all value needs to be included in a string
❗❗ all css properties needs to adopt the camelCase notation no dash allowed

2 ways of getting an element by its ID:

```js
const score1 = document.getElementById("score--0");
const score1 = document.querySelector("#score--0");
```

Toggling between CSS classes:

```js
const openModal = function () {
  modal.classList.remove("hidden");
  overlay.classList.remove("hidden");
};

const closeModal = function () {
  modal.classList.add("hidden");
  overlay.classList.add("hidden");

  player0El.classList.toggle("player--active");
};
```
