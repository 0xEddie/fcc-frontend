## 04-Dec-2023
### CSS overflow
A box in a box in a frame

```html
<html>
<body>
  <div class="frame">
    <div class="canvas">
      <div class="one"></div>
    </div>
  </div>
</body>
```

```css
.frame {
  border: 50px solid black;
  width: 500px;
  padding: 50px;
  margin: 20px auto;
}

canvas {
  width: 500px;
  height: 600px;
  background-color: #4d0f00;
}

.one {
  width: 425px;
  height: 150px;
  background-color: #efb762;
}
```

![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/68651656-4afd-4b9d-bd3e-ffb4ee7b2a16)

However when we add some margin to `.one` to bump it down in `.canvas` and center it horizontally, something funny happens.

```css
.one {
  width: 425px;
  height: 150px;
  background-color: #efb762;
  margin: 20px auto;
}
```

![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/cb302301-8778-458c-a35b-736f5d30e8a1)

We can see (using browser dev tools) that the child box (`.one`) is pushing away from `.frame`, not `.canvas`
![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/bcfede9f-1216-4cc4-a411-4b4048a70d57)
![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/c532e6a2-6d73-4cc4-8b9e-0f9bc1e192e0)

Margin collapse is a phenomenon in CSS where the margins of adjacent elements can overlap or combine under certain conditions, resulting in a different margin than what might be expected intuitively.

Margin collapse occurs primarily with vertical margins of block-level elements that are stacked one after another.

Margins collapse occurs on specific conditions:
- Margins of adjacent siblings (block-level elements that are direct children of the same parent).
- Empty blocks or blocks with no border, padding, or content to separate their margins.
- Parent and first/last child element margins.

Preventing margin collapse:
- On the parent element, add padding, borders, or use certain CSS properties like `overflow: hidden;`, `float`, or `display: inline-block;`
- Sometimes changing the display property (e.g., from block to inline-block) can prevent collapse.

We can either add padding to the top of the `.canvas` box
```css
.canvas {
canvas {
  width: 500px;
  height: 600px;
  background-color: #4d0f00;
  padding-top: 50px;
}
```

![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/acbd56a3-bd0a-46c0-a676-6a0f86c698bb)

Or if we don't want to alter the box padding, we can change the `overflow` property from the default `visible` value.

`overflow: hidden;` will clip content that extends beyond its border, but more usefully for us is that it establishes a new **BFC (Block Formatting Context)**, which isolates the margins of child elements from affecting the layout of the parent elements. In other words, it forces the child `.one` box to use the `.canvas`'s border as a wall, instead of allowing `.ones`'s margin to merge with `.canvas`'s margin.
```css
.canvas {
canvas {
  width: 500px;
  height: 600px;
  background-color: #4d0f00;
  overflow: hidden;
}
```

![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/20029406-2677-4cc1-bcfe-7a9c75322c1d)

## 05 Dec 2023
### CSS content box sizing
Building a little cat photo gallery
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Photo Gallery</title>
    <link rel="stylesheet" href="./styles.css">
  </head>
  <body>
    <header class="header">
      <h1>css flexbox photo gallery</h1>
    </header>
    <div class="gallery">
      <img src="https://cdn.freecodecamp.org/curriculum/css-photo-gallery/1.jpg">
      <img src="https://cdn.freecodecamp.org/curriculum/css-photo-gallery/2.jpg">
      <img src="https://cdn.freecodecamp.org/curriculum/css-photo-gallery/3.jpg">
      <img src="https://cdn.freecodecamp.org/curriculum/css-photo-gallery/4.jpg">
    </div>
  </body>
</html>
```

```css
.gallery {
  width: 50%;
  border: 5px solid red;
}
img {
  width: 100%;
  padding: 5px;
  border: 5px solid blue;
}
```

We see the border and padding of each image element is overflowing outside of the parent gallery element.

![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/49305584-df43-4167-9b32-b64dc469d8b6)

Putting `overflow:hidden` on the parent `.gallery` doesn't even fix this, it only chops off the offending pixels.
```css
.gallery {
  ...
  overflow: hidden;
}
```
![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/99b46399-d919-4a4d-91f0-479b300e0f1e)

The `box-sizing` CSS property sets how the total width and height of an element is calculated.

The default value is `content-box` and ONLY includes the content for calculating the width and height, it does NOT include the padding or border (or margin).

The other interesting value is `border-box` which then includes the padding and border thickness in calculating the size of the content (still doesn't include margin).

So one way to fix our overflowing photos is to throw `box-sizing: border-box;` onto the image elements.

```css
img {
  ...
  box-sizing: border-box;
}
```
![image](https://github.com/0xEddie/fcc-frontend/assets/36518273/0f4d5bb3-b46b-4832-b81e-68519c8a6f17)
