---
title: Input tag
category: HTML
updated: 2017-10-30
---

### Input

```html
 <input ...
   disabled
   required
   checked
```

```html
autofocus
```

```html
autocomplete='off'
<!-- autocomplete -->
autocompletetype='cc-exp' autocapitalize='off'
<!-- for mobiles -->
pattern='\d*'
<!-- force numeric input in iOS -->
```

### Input types

#### Text

- email
- hidden
- **password**
- tel
- **text**
- search

#### Time

- date
- time

#### Time (not widely supported)

- month
- week
- datetime
- datetime-local

#### Etc

- **file**
- **radio**
- **checkbox**

#### Buttons

- button
- reset
- submit
- image

#### Numeric

- number
- range

## Examples

### Dates

| Type          | Example             |
| ------------- | ------------------- |
| `type='date'` | <input type='date'> |
| `type='time'` | <input type='time'> |

### Datetime

| Type                    | Example                       |
| ----------------------- | ----------------------------- |
| `type='datetime'`       | <input type='datetime'>       |
| `type='datetime-local'` | <input type='datetime-local'> |

`datetime` and `datetime-local` fields are not widely supported.

### Numbers

| Type            | Example               |
| --------------- | --------------------- |
| `type='number'` | <input type='number'> |
| `type='range'`  | <input type='range'>  |

### Text

| Type              | Example                 |
| ----------------- | ----------------------- |
| `type='text'`     | <input type='text'>     |
| `type='password'` | <input type='password'> |
| `type='search'`   | <input type='search'>   |
| `type='tel'`      | <input type='tel'>      |

## Also see

- <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input>

## Forms and Labels

It is industry standard to wrap `input` tags in `label` tags

```html
<form action="https://www.freecatphotoapp.com/submit-cat-photo">
  <label for="indoor"
    ><input id="indoor" type="radio" name="indoor-outdoor" value="indoor" />
    Indoor</label
  >
  <label for="outdoor"
    ><input id="outdoor" type="radio" name="indoor-outdoor" value="outdoor" />
    Outdoor</label
  ><br />
  <label for="loving"
    ><input id="loving" type="checkbox" name="personality" value="loving" />
    Loving</label
  >
  <label for="lazy"
    ><input id="lazy" type="checkbox" name="personality" value="lazy" />
    Lazy</label
  >
  <label for="energetic"
    ><input
      id="energetic"
      type="checkbox"
      name="personality"
      value="energetic"
    />
    Energetic</label
  ><br />
  <input type="text" placeholder="cat photo URL" required />
  <button type="submit">Submit</button>
</form>
```

Also the attributes added in the input tags above should be specified if the inputs should return values to the server. In which case, all input and label tags should be wrapped into `form` tags and a `submit` button should be added too.

The action attribute specifies where the data should be sent once submitted.
