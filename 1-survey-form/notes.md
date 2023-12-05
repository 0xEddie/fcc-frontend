## 18-Nov-2023
- In anchor tags, set attribute `target="_blank"` to open link in a new tab. Does this apply for all values of `target`?
- In form elements, the `action` attribute is set to the value the URL the form data will be submitted to
`<label><input type="radio"> cat~</label>`
  - `label` elements will associate the text for an `input` element with the `input` label itself

- form data for buttons is based on `name` and `value` attributes
```html
<label><input id="indoor" type="radio" name="indoor-outdoor">Indoor</label>
<label><input id="outdoor" type="radio" name="indoor-outdoor">Outdoor</label>
```
  - since these radio buttons have no `value` attribute, the form data will include (default) `indoor-outdoor=on`
  - not helpful if you have multiple buttons!
  - for convenience, set `value` of radio buttons to their `id` attribute
- don't have to wrap `input` elements in `label` to make its text clickable
  - can also wrap only text in `label` but give `label` the `for` attribute, and set it it to the same value as the `input`'s `id` attribute
```html
<input id="loving" type="checkbox" name="personality" value="loving" checked> <label for="loving">Loving</label>
<input id="lazy" type="checkbox" name="personality" value="lazy"> <label for="lazy">Lazy</label>
```
-  `fieldset` elements are block-level elements, used to group related sections of elements together in forms
- `legend` is a caption/description for a `fieldset`

![image](https://github.com/0xEddie/cool-tools/assets/36518273/e3f5b628-ef80-4e7c-ad93-985679ea7b47)

## 20-Nov-2023
- Primary colors
  - one of RGB is set to max (255) in an RBG function: `rgb(255, 0, 0)`
- Secondary colors
  - two of RGB are maxed in an RGB function `rgb(0, 255, 255)`
- Tertiary colors
  - one color is maxed, combined with a second color at half intensity `rgb(0, 255, 127)`
- Complementary colors
  - Two colors opposite each other on the color wheel
  - When combined will create gray
  - When side by side, will contrast and appear brighter
    - text on a complementary background is hard to read
      ```css
      p {
        color: rgb(255, 0, 0);
        background-color: rgb(0, 255, 255);
      }
      ```
- Colors can also be expressed in CSS in either hexadecimal or HSL (hue, saturation, lightness
  - `color: #007F00;`
  - `color: hsl(240, 100%, 50%)`
- the `linear-gradient` function actually creates an `image` element, and is usually paired with the `background` property which can accept an image as a value `background: linear-gradient(90deg, rgb(255, 0, 0), rgb(0, 255, 0))`
-  in this red-black gradient, the transition from red to black takes place at the 90% point along the gradient line (so red takes up 90% of the space) `linear-gradient(90deg, red 90%, black);`
  
## 21-Nov-2023
- Not sure why this wasn't obvious to me, but complex shapes can be drawn by just placing `div`s inside other `div`s
![image](https://github.com/0xEddie/cool-tools/assets/36518273/47450bbb-ef5c-4cf9-bfa7-c1a17d092e84)

```html
<div class="container">
  <div class="marker red">
    <div class="cap"></div>
    <div class="sleeve"></div>
  </div>
  <div class="marker green">
    <div class="cap"></div>
    <div class="sleeve"></div>
  </div>
</div>
```
```css
.container {
  background-color: rgb(255, 255, 255);
  padding: 10px 0;
}

.marker {
  width: 200px;
  height: 25px;
  margin: 10px auto;
}

.cap {
  width: 60px;
  height: 25px;
}

.sleeve {
  width: 110px;
  height: 25px;
  background-color: rgba(255, 255, 255, 0.5);
  border-left: 10px double rgba(0, 0, 0, 0.75);
}

.cap, .sleeve {
  display: inline-block;
}

.red {
  background: linear-gradient(rgb(122, 74, 14), rgb(245, 62, 113), rgb(162, 27, 27));
}

.green {
  background: linear-gradient(#55680D, #71F53E, #116C31);
}
```
- A subtle pop of emphasis for elements is to use the `box-shadow` CSS function `box-shadow: offsetX offsetY blurRadius spreadRadius color;`
  - `offsetX` & `offsetY` are measured from the top left corner of an element
  - `blurRadius` & `spreadRadius` are optional and default to `0`
```css
.green {
  background: linear-gradient(#55680D, #71F53E, #116C31);
  box-shadow: 0 0 20px 0 #3B7E20CC;
}
```
![image](https://github.com/0xEddie/cool-tools/assets/36518273/954004f6-64a8-4f9c-a051-16ba8965768f)

## 22-Nov-2023
- Oh my gooooood the difference between GET and POST is how the data is sent in the request, either in the URL (with GET requests) or in the request body (via POST requests).
- The method attribute specifies how to send form-data to the URL specified in the action attribute. The form-data can be sent via a GET request as URL parameters (with method="get") or via a POST request as data in the request body (with method="post").
`    <form action='https://register-demo.freecodecamp.org' method="post"></form>`
- For forms with a required section with `radio` button toggles, you can't just slap a `required` attribute on every radio button (because only one radio can be selected in a related group at any time). However, you can label one radio with `checked` attribute, then optionally add a `legend` caption at the start of the group.
```html
<fieldset>
  <legend>Account type (required)</legend>
  <label><input type="radio" name="account-type" checked /> Personal</label>
  <label><input type="radio" name="account-type" /> Business</label>
</fieldset>
```
(using best practices for accessbility, attaching the label to its respective radio button)
```html
<fieldset>
  <legend>Account type (required)</legend>
  <label for="personal-account"><input id="personal-account" type="radio" name="account-type" checked /> Personal</label>
  <label for="business-account"><input id="business-account" type="radio" name="account-type" /> Business</label>
</fieldset>
```
- During development, it is useful to see the fieldset default borders. However, they visually separate content quite harshly.
![image](https://github.com/0xEddie/cool-tools/assets/36518273/c3b98484-603f-4be0-a905-f447500286eb)
```css
fieldset {
  border: none;
  padding: 2rem 0;
  border-bottom: 3px solid #3b3b4f;
}

fieldset:last-of-type {
  border-bottom: none;
}
```
![image](https://github.com/0xEddie/cool-tools/assets/36518273/f59b5398-efc9-4d0c-9794-18bab7970cfc)

## 28-Nov-2023
- You can use attributes of HTML elements as CSS selectors
```css
input[type="submit"] {}
input[name="email"] {}
```
