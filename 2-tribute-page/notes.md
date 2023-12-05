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
