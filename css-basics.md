---
title: CSS Basics
category: CSS
---

## Basics

### Selectors

| Selector          | Description  |
| ----------------- | ------------ |
| `*`               | All elements |
| `div`             | Element      |
| `.class`          | Class        |
| `#id`             | ID           |
| `[disabled]`      | Attribute    |
| `[role="dialog"]` | Attribute    |

### Combinators

| Selector            | Description       |
| ------------------- | ----------------- |
| `.parent .child`    | Descendant        |
| `.parent > .child`  | Direct descendant |
| `.child + .sibling` | Adjacent sibling  |
| `.child ~ .sibling` | Far sibling       |
| `.class1.class2`    | Have both classes |

### Attribute selectors

| Selector           | Description                         |
| ------------------ | ----------------------------------- |
| `[role="dialog"]`  | `=` Exact                           |
| `[class~="box"]`   | `~=` Has word                       |
| `[class|="box"]`   | `|=` Exact or prefix (eg, `value-`) |
| `[href$=".doc"]`   | `$=` Ends in                        |
| `[href^="/index"]` | `^=` Begins with                    |
| `[class*="-is-"]`  | `*=` Contains                       |

### Pseudo-classes

| Selector             | Description                                |
| -------------------- | ------------------------------------------ |
| `:target`            | eg, `h2#foo:target`                        |
| `:disabled`          |                                            |
| `:focus`             |                                            |
| `:active`            |                                            |
| `:nth-child(3)`      | 3rd child                                  |
| `:nth-child(3n+2)`   | 2nd child in groups of 3                   |
| `:nth-child(-n+4)`   |                                            |
| `:nth-last-child(2)` |                                            |
| `:nth-of-type(2)`    |                                            |
| `:checked`           | Checked inputs                             |
| `:disabled`          | Disabled elements                          |
| `:default`           | Default element in a group                 |
| `:empty`             | Elements without children                  |

### Pseudo-class variations

| Selector          |
| ----------------- |
| `:first-of-type`  |
| `:last-of-type`   |
| `:nth-of-type(2)` |
| `:only-of-type`   |
| `:first-child`    |
| `:last-child`     |
| `:nth-child(2)`   |
| `:only-child`     |
{: .-left-align}

## Fonts

### Properties

| Property           | Description                          |
| ------------------ | ------------------------------------ |
| `font-family:`     | `<font>, <fontN>`                    |
| `font-size:`       | `<size>`                             |
| `letter-spacing:`  | `<size>`                             |
| `line-height:`     | `<number>`                           |
| `font-weight:`     | `bold` `normal`                      |
| `font-style:`      | `italic` `normal`                    |
| `text-decoration:` | `underline` `none`                   |
| `text-align:`      | `left` `right` `center` `justify`    |
| `text-transform:`  | `capitalize` `uppercase` `lowercase` |

### Example

```css
font-family: Arial;
font-size: 12pt;
line-height: 1.5; /*NO UNIT */
letter-spacing: 0.02em;
color: #aa3322;
```

### Case

```css
text-transform: capitalize; /* Hello */
text-transform: uppercase; /* HELLO */
text-transform: lowercase; /* hello */
```

## Background

### Properties

| Property                 | Description                              |
| ------------------------ | ---------------------------------------- |
| `background:`            | _(Shorthand)_                            |
| `background-color:`      | `<color>`                                |
| `background-image:`      | `url(...)`                               |
| `background-position:`   | `left/center/right` `top/center/bottom`  |
| `background-size:`       | `cover` `X Y`                            |
| `background-clip:`       | `border-box` `padding-box` `content-box` |
| `background-repeat:`     | `no-repeat` `repeat-x` `repeat-y`        |
| `background-attachment:` | `scroll` `fixed` `local`                 |

### Shorthand

|               | color  | image         | positionX | positionY |     | size           | repeat      | attachment |
| ------------- | ------ | ------------- | --------- | --------- | --- | -------------- | ----------- | ---------- |
| `background:` | `#ff0` | `url(bg.jpg)` | `left`    | `top`     | `/` | `100px` `auto` | `no-repeat` | `fixed;`   |
| `background:` | `#abc` | `url(bg.png)` | `center`  | `center`  | `/` | `cover`        | `repeat-x`  | `local;`   |

### Multiple backgrounds

```css
background: linear-gradient(to bottom, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
  url('background.jpg') center center / cover, #333;
```

## Animation

### Properties

| Property                     | Value                                                    |
| ---------------------------- | -------------------------------------------------------- |
| `animation:`                 | _(shorthand)_                                            |
| `animation-name:`            | `<name>`                                                 |
| `animation-duration:`        | `<time>ms`                                               |
| `animation-timing-function:` | `ease` `linear` `ease-in` `ease-out` `ease-in-out`       |
| `animation-delay:`           | `<time>ms`                                               |
| `animation-iteration-count:` | `infinite` `<number>`                                    |
| `animation-direction:`       | `normal` `reverse` `alternate` `alternate-reverse`       |
| `animation-fill-mode:`       | `none` `forwards` `backwards` `both` `initial` `inherit` |
| `animation-play-state:`      | `normal` `reverse` `alternate` `alternate-reverse`       |

### Shorthand

|              | name     | duration | timing-function | delay   | count      | direction           | fill-mode | play-state |
| ------------ | -------- | -------- | --------------- | ------- | ---------- | ------------------- | --------- | ---------- |
| `animation:` | `bounce` | `300ms`  | `linear`        | `100ms` | `infinite` | `alternate-reverse` | `both`    | `reverse`  |

### Example

```css
animation: bounce 300ms linear 0s infinite normal;
animation: bounce 300ms linear infinite;
animation: bounce 300ms linear infinite alternate-reverse;
animation: bounce 300ms linear 2s infinite alternate-reverse forwards normal;
```

### Variables

```scss
:root {
  --text-color: #30333a;
}
```

```scss
body {
  background: var(--text-color);
  background: color(var(--text-color) shade(30%));
}
```

### Colors

```scss
a {
  /* Adjustments */
  color: color(red alpha(-10%));
  color: color(red tint(-10%));    /* lighten */
  color: color(red shade(-10%));   /* darken */

  /* Absolute */
  color: color(red alpha(50%));
  color: color(red hue(225));
  color: color(red saturation(100%));
  color: color(red lightness(50%));

  color: gray(33);       /* rgb(33, 33, 33) */
  color: gray(33%);      /* rgb(84, 84, 84) */
  color: gray(33%, 50%); /* rgba(84, 84, 84, 0.5) */
  color: #0000ff80;      /* rgba(0, 0, 255, 0.5) */

  color: hwb(90, 0%, 0%, 0.5);     /* like hsl() but easier for humans */
  color: hsl(90deg 90% 70%);       /* hsl(180, 90%, 70%) -- supports deg */
  color: hsl(90deg 90% 70% / 30%); /* hsla(180, 90%, 70%, 0.3) */
  color: rgb(30 60 90 / 30%);      /* rgba(30, 60, 90, 0.3) */
}
```

Also see [colorme.io](http://colorme.io/).

### Mixins

```scss
:root {
  --centered: {
    display: flex;
    align-items: center;
    justify-content: center;
  };
}

.centered {
  @apply --centered;
}