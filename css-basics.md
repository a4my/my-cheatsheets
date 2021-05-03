---
title: CSS Basics
category: CSS
---

## Basics

### Basic Selectors

<table>
  <tbody>
  <tr>
    <th>Selector</th>
    <th>Example</th>
    <th>Example description</th>
  </tr>
  <tr>
    <td>.<i>class</i></td>
    <td>.intro</td>
    <td>Selects all elements with class="intro"</td>
  </tr>
  <tr>
    <td>#<i>id</i></td>
    <td>#firstname</td>
    <td>Selects the element with id="firstname"</td>
  </tr>
  <tr>
    <td>*</td>
    <td>*</td>
    <td>An asterisk (*) is the universal selector for CSS. It matches a single element of any type. Omitting the asterisk with simple selectors has the same effect. For instance, `*.warning` and `.warning` are considered equal.
    </td>
  </tr>
  <tr>
    <td><i>element</i></td>
    <td>p</td>
    <td>CSS type selectors match elements by node name. In the example, it selects all &lt;p&gt; elements</td>
  </tr>
  <tr>
    <td><i>element,element</i></td>
    <td>div, p</td>
    <td>Selects all &lt;div&gt; elements and all &lt;p&gt; elements</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>]</td>
    <td>[target]</td>
    <td>Selects all elements with a target attribute</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>=<i>value</i>]</td>
    <td>[target=_blank]</td>
    <td>Selects all elements with target="_blank"</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>~=<i>value</i>]</td>
    <td>[title~=flower]</td>
    <td>Selects all elements with a title attribute containing the word "flower"</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>|=<i>value</i>]</td>
    <td>[lang|=en]</td>
    <td>Selects all elements with a lang attribute value starting with "en"</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>^=<i>value</i>]</td>
    <td>a[href^="https"]</td>
    <td>Selects every &lt;a&gt; element whose href attribute value begins with "https"</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>$=<i>value</i>]</td>
    <td>a[href$=".pdf"]</td>
    <td>Selects every &lt;a&gt; element whose href attribute value ends with ".pdf"</td>
  </tr>
  <tr>
    <td>[<i>attribute</i>*=<i>value</i>]</td>
    <td>a[href*="motorhead"]</td>
    <td>Selects every &lt;a&gt; element whose href attribute value contains the substring
  "motorhead"</td>
  </tr>
  </tbody>
</table>


### Combinators

<table>
  <tbody>
  <tr>
    <th>Selector</th>
    <th>Example</th>
    <th>Example description</th>
  </tr>
  <tr>
    <td><i>element</i> <i>element</i></td>
    <td>div p</td>
    <td>Descendant selector. Selects all &lt;p&gt; elements inside &lt;div&gt; elements. </td>
  </tr>
  <tr>
    <td><i>element</i>&gt;<i>element</i></td>
    <td>div &gt; p</td>
    <td>Child selector. Selects all &lt;p&gt; elements where the parent is a &lt;div&gt; element. The difference between the standard X Y and X &gt; Y is that the latter will only select direct children.</td>
  </tr>
  <tr>
    <td><i>element</i>+<i>element</i></td>
    <td>div + p</td>
    <td>Adjacent selector or next-sibling selector.  It will select only the specified element that immediately follows the former specified element. In this example, it selects all &lt;p&gt; elements that are placed immediately after &lt;div&gt; elements</td>
  </tr>
  <tr>
    <td><i>element1</i>~<i>element2</i></td>
    <td>p ~ ul</td>
    <td>General sibling selector. Selects every &lt;ul&gt; element that are preceded by a &lt;p&gt; element</td>
  </tr>
  </tbody>
</table>


### Pseudo-elements

Pseudo-elements are added to selectors but instead of describing a special state, they allow you to style certain parts of a document. For example, the `::first-line` pseudo-element targets only  the first line of an element specified by the selector.

<table>
  <tbody>
  <tr>
    <th>Selector</th>
    <th>Example</th>
    <th>Example description</th>
  </tr>
  <tr>
    <td>s::after</td>
    <td>p::after</td>
    <td>Insert something after the content of each &lt;p&gt; element</td>
  </tr>
  <tr>
    <td>::before</td>
    <td>p::before</td>
    <td>Insert something before&nbsp;the content of each &lt;p&gt; element</td>
  </tr>
  <tr>
    <td>::first-letter</td>
    <td>p::first-letter</td>
    <td>Selects the first letter of every &lt;p&gt; element</td>
  </tr>
  <tr>
    <td>::first-line</td>
    <td>p::first-line</td>
    <td>Selects the first line of every &lt;p&gt; element</td>
  </tr>
  <tr>
    <td>::selection</td>
    <td>::selection</td>
    <td>Selects the portion of an element that is selected by a user</td>
  </tr>
  </tbody>
</table>

### Pseudo-classes

A CSS pseudo-class is a keyword added to selectors that specifies a special state of the element to be selected. For example `:hover` will apply a style when the user hovers over the element specified by the selector.

<table>
  <tbody>
  <tr>
    <th>Selector</th>
    <th>Example</th>
    <th>Example description</th>
  </tr>
  <tr>
    <td>:active</td>
    <td>a:active</td>
    <td>Selects the active link</td>
  </tr>
  <tr>
    <td>:checked</td>
    <td>input:checked</td>
    <td>Selects every checked &lt;input&gt; element</td>
  </tr>
  <tr>
    <td>:disabled</td>
    <td>input:disabled</td>
    <td>Selects every disabled &lt;input&gt; element</td>
  </tr>
  <tr>
    <td>:empty</td>
    <td>p:empty</td>
    <td>Selects every &lt;p&gt; element that has no children (including text nodes)</td>
  </tr>
  <tr>
    <td>:enabled</td>
    <td>input:enabled</td>
    <td>Selects every enabled &lt;input&gt; element</td>
  </tr>
  <tr>
    <td>:first-child</td>
    <td>p:first-child</td>
    <td>Selects every &lt;p&gt; element that is the first child of its parent</td>
  </tr>
  <tr>
    <td>:first-of-type</td>
    <td>p:first-of-type</td>
    <td>Selects every &lt;p&gt; element that is the first &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:focus</td>
    <td>input:focus</td>
    <td>Selects the input element which has focus</td>
  </tr>
  <tr>
    <td>:hover</td>
    <td>a:hover</td>
    <td>Selects links on mouse over</td>
  </tr>
  <tr>
    <td>:in-range</td>
    <td>input:in-range</td>
    <td>Selects input elements with a value within a specified range</td>
  </tr>
  <tr>
    <td>:invalid</td>
    <td>input:invalid</td>
    <td>Selects all input elements with an invalid value</td>
  </tr>
  <tr>
    <td>:lang(<i>language</i>)</td>
    <td>p:lang(it)</td>
    <td>Selects every &lt;p&gt; element with a lang attribute equal to "it"
  (Italian)</td>
  </tr>
  <tr>
    <td>:last-child</td>
    <td>p:last-child</td>
    <td>Selects every &lt;p&gt; element that is the last child of its parent</td>
  </tr>
  <tr>
    <td>:last-of-type</td>
    <td>p:last-of-type</td>
    <td>Selects every &lt;p&gt; element that is the last &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:link</td>
    <td>a:link</td>
    <td>Selects all unvisited links</td>
  </tr>
  <tr>
    <td>:not(<i>selector</i>)</td>
    <td>:not(p)</td>
    <td>Selects every element that is not a &lt;p&gt; element</td>
  </tr>
  <tr>
    <td>:nth-child(<i>n</i>)</td>
    <td>p:nth-child(2)</td>
    <td>Selects every &lt;p&gt; element that is the second child of its parent</td>
  </tr>
  <tr>
    <td>:nth-last-child(<i>n</i>)</td>
    <td>p:nth-last-child(2)</td>
    <td>Selects every &lt;p&gt; element that is the second child of its parent, counting
  from the last child</td>
  </tr>
  <tr>
    <td>:nth-last-of-type(<i>n</i>)</td>
    <td>p:nth-last-of-type(2)</td>
    <td>Selects every &lt;p&gt; element that is the second &lt;p&gt; element of its parent, counting
  from the last child</td>
  </tr>
  <tr>
    <td>:nth-of-type(<i>n</i>)</td>
    <td>p:nth-of-type(2)</td>
    <td>Selects every &lt;p&gt; element that is the second &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:only-of-type</td>
    <td>p:only-of-type</td>
    <td>Selects every &lt;p&gt; element that is the only &lt;p&gt; element of its
  parent</td>
  </tr>
  <tr>
    <td>:only-child</td>
    <td>p:only-child</td>
    <td>Selects every &lt;p&gt; element that is the only child of its parent</td>
  </tr>
  <tr>
    <td>:optional</td>
    <td>input:optional</td>
    <td>Selects input elements with no "required" attribute</td>
  </tr>
  <tr>
    <td>:out-of-range</td>
    <td>input:out-of-range</td>
    <td>Selects input elements with a value outside a specified range</td>
  </tr>
  <tr>
    <td>:read-only</td>
    <td>input:read-only</td>
    <td>Selects input elements with the "readonly" attribute specified</td>
  </tr>
  <tr>
    <td>:read-write</td>
    <td>input:read-write</td>
    <td>Selects input elements with the "readonly" attribute NOT specified</td>
  </tr>
  <tr>
    <td>:required</td>
    <td>input:required</td>
    <td>Selects input elements with the "required" attribute specified</td>
  </tr>
  <tr>
    <td>:root</td>
    <td>:root</td>
    <td>Selects the document's root element</td>
  </tr>
  <tr>
    <td>:target</td>
    <td>#news:target </td>
    <td>Selects the current active #news element (clicked on a URL containing that anchor name)</td>
  </tr>
  <tr>
    <td>:valid</td>
    <td>input:valid</td>
    <td>Selects all input elements with a valid value</td>
  </tr>
  <tr>
    <td>:visited</td>
    <td>a:visited</td>
    <td>Selects all visited links</td>
  </tr>
  </tbody>
</table>


## Animation

```css
.element {
  animation: pulse 5s infinite;
}

@keyframes pulse {
  0% {
    background-color: #001F32;
  }
  100% {
    background-color: #D41368;
  }
}
```

## Sub-properties

```css
.element {
  animation-name: stretch;
  animation-duration: 1.5s;
  animation-timing-function: ease-out;
  animation-delay: 0;  //Specifies a delay for the start of an animation
  animation-direction: alternate;  //Specifies whether an animation should play in reverse direction or alternate cycles
  animation-iteration-count: infinite;
  animation-fill-mode: none;
  animation-play-state: running;
}

```

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