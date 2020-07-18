---
layout: post
title: 'Flexbox basics 1/2'
date: 2020-07-17 11:49:30 +0900
categories: css flexbox
---

Flexbox makes laying out pages with CSS a breeze. It is usable in prety much [all browsers](https://caniuse.com/#feat=flexbox){:target="\_blank"}, so if you haven't been able to get your head around it yet or are just looking for a quick refresher, I hope this helps.
If you're used to using floats to align elements on a page you'll know how finicky and hard to work with they are for all but the most simple cases. Flexbox offers an alternative, and while it can handle 2D or table-like layouts, it is most suited for one dimensional (row/column) layouts.

In this first of two posts I'll be explaining the different CSS properties available to the outer flex container, and in the second post I'll be covering the properties of the contained flex items.

## The Container

### display:flex

To start using flexbox, you'll first need a container or wrapper item that will act as the parent to the elements within. In terms of tables you could think of the container as a 'row' and the elements as 'cells' although unlike rows in a table, items in a flexbox can be lined up vertically as well as horizontally as we'll see later. Defining an element as your flex container is as simple as setting `display` to `flex` in its css.

```html
<div style="display:flex">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
  <div>Item 5</div>
</div>
```

<div style="display:flex">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
  <div>Item 5</div>
</div>
<br />
You might have noticed that just by defining `display:flex` on the container, we're already seeing the effects of flexbox.
Without `display:flex` we'd be getting a vertical column of divs. With it, they line up horizontally in a row.
That's because flexbox displays elements in a row by default.

### flex-direction

The flexbox property responsible for this is called `flex-direction`, and by setting it to `column`, we can arrange the elements vertically instead.

```html
<div style="display:flex; flex-direction: column;">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
  <div>Item 5</div>
</div>
```

<div style="display:flex; flex-direction: column;">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
  <div>Item 4</div>
  <div>Item 5</div>
</div>
<br />
There are also reversed versions of both the `row` and `column` flex-directions, `row-reverse` and `column-reverse`, which display elements in reverse order.

## Alignment and Justification

Before we talk about alignment and justification, we need to discuss axes.
Every flexbox layout has a main axis and a cross axis.
The main axis is axis that runs along the flex-direction, and the cross axis is the axis perpendicular to it.

|            | `flex-direction: row`                                                 | `flex-direction: column`                                                    |
| ---------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Main axis  | horizontal                                                            | vertical                                                                    |
| Cross axis | vertical                                                              | horizontal                                                                  |
|            | ![flex-direction: row](/assets/2020-07-17-flexbox-basics/flexrow.png) | ![flex-direction: column](/assets/2020-07-17-flexbox-basics/flexcolumn.png) |

Whenever you see the word 'justify', think main axis.
So for a row flexbox layout, to make all the elements bunch up to the left or right, you would use justify-content.
Conversely when you see the word 'align', think cross axis.
Again for a row layout, to make all the elements move to the top or bottow, you would use align-content.

### justify-content

As you may now be able to guess, `justify-content` is the property used to specify alignment along the main axis, and its values are as follows:

`flex-start` (default): Elements are aligned to the start of the axis. For a row layout, this would be to the left, and for a column layout, at the top. Note that the 'start' is reverse when using a reversed direction. For example for a `row-reverse` flex direction, `flex-start` would be to the right side instead of left.

<div style="display: flex;width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`flex-end`: The opposite of `flex-start`, elements are align from the end of the axis.

<div style="display: flex; justify-content: flex-end; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`center`: Elements all bunch up in the center of the axis.

<div style="display: flex; justify-content: center; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`space-between`: Elements are arranged so that the space between each of them along the axis is identical.

<div style="display: flex; justify-content: space-between; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`space-around`: Elements are arranged so that they all have the same space around them, similar to if you set the same padding on each of them.

<div style="display: flex; justify-content: space-around; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`space-evenly`: Simlar to `space-between`, but with spaces at either end of the axis as well.

<div style="display: flex; justify-content: space-evenly; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

### align-items

`align-items` allows you align items along the cross axis. `center` `flex-start` `flex-end` work much the same as they do for `justify-content`. The default value of `align-items` is `stretch` which stretches items to the full width or height of the container along the cross axis.

`flex-direction: row; align-items: stretch`

<div style="display: flex; justify-content: space-evenly; align-items: stretch; width: 500px; height: 100px; padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`flex-direction: row; align-items: flex-start`

<div style="display: flex; justify-content: space-evenly; align-items: flex-start; width: 500px; height: 100px; padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

`flex-direction: row; align-items: center`

<div style="display: flex; justify-content: space-evenly; align-items: center; width: 500px; height: 100px; padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;">Item 1</div>
  <div style="background-color: #223344;color: white;">Item 2</div>
  <div style="background-color: #223344;color: white;">Item 3</div>
</div><br/>

### align-content

Somewhat confusingly, as well as an `align-items` property, there also is a property named `align-content`.
`align-content` comes into effect when you have more than one row/column of items along the cross axis which can happen if you allow your items to wrap with the `flex-wrap: wrap` property.
`align-content` works in much the same way and has the same possible values as `justify-content`.

`align-content: flex-start`

<div style="display: flex; justify-content: space-evenly; align-items: center; align-content: flex-start; width: 500px; height: 100px; padding: 5px; background-color: #f2f2f2f2; flex-wrap: wrap;">
  <div style="background-color: #223344;color: white; width: 120px;">Item 1</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 2</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 3</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 4</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 5</div>
  <div style="background-color: #223344;color: white; width: 100px;">Item 6</div>
</div><br/>

`align-content: space-between`

<div style="display: flex; justify-content: space-evenly; align-items: center; align-content: space-between; width: 500px; height: 100px; padding: 5px; background-color: #f2f2f2f2; flex-wrap: wrap;">
  <div style="background-color: #223344;color: white; width: 120px;">Item 1</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 2</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 3</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 4</div>
  <div style="background-color: #223344;color: white; width: 120px;">Item 5</div>
  <div style="background-color: #223344;color: white; width: 100px;">Item 6</div>
</div><br/>

Well that about covers flexbox properties set on the container, in the next post we'll take a look at the various flexbox properties available on the items themselves that give you even more control over positioning.

{% include share-buttons.html %}
