---
title: CSS tricks
category: CSS
---

### Gradient text

```css
background: -webkit-gradient(linear, left top, left bottom, from(#eee), to(#333));
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

### Text stroke

```css
-webkit-text-stroke: 3px black;
```

### shadows

• for pngs, shapes and icons:

```css
filter: drop-shadow(2px 1px 2px rgba(0, 0, 0, 99));
```

• text:

```css
text-shadow: 2px 1px 2px rgba(0, 0, 0, 99);
```

• containers (div, main, section, etc)

```css
box-shadow: 2px 1px 2px rgba(0, 0, 0, 99);
```

### Blur effect

```css
backdrop-filter: blur(6px);
```

• Neumorphism:

```css
box-shadow: 13px 13px 20px var(--shadow--1), 
            -13px -13px 20px var(--shadow--2);
```