---
layout: post
title: "Customizing the native HTML date input"
date: 2021-08-22 08:49:30 +0900
categories: css
---

### About the native HTML date input and differences between browsers/OS's

The native HTML date input of which there are a number of variations (date, datetime-local, etc.), allows users to enter a date, and has styling that is determined by the client OS and browser.

| iOS/Safari | Android/Chrome | PC/Chrome |
| ---------- | -------------- | --------- |


In addition, as of the writing of this post, the events fired by the native date pickers provided by iOS and Android differ in the following way.

|                            | iOS      | Android  |
| -------------------------- | -------- | -------- |
| Date changed within picker | onChange | none     |
| Picker closed              | blur     | onChange |

For a simple form this may not make a difference but if you have some data you want to update whenever the date changes, you have a bit of a problem.
If you request the new data from the server in the onChange event, you'll end up making unneeded requests on iOS as the user scrolls through months and days. (You could debounce the onChange events to somewhat improve things but this is still not ideal).
If you instead tie the server update to the blur event, you won't get any updates on Android at all.
Unfortunately this may be a case where to get a consistent experience browser sniffing may be the best option.

While this makes it a challenge to provide a consistent look and feel across different platforms, we are not without options.

<p styled="padding: 10px; background: #f2f2f2; opacity: 0.8;">
On a PC or Mac, the features of the native date input are very basic so I would recommend also considering a dedicated date picker plugin such as [react-dates](https://github.com/airbnb/react-dates){:target="\_blank"} or [blueprint datetime](https://github.com/palantir/blueprint){:target="\_blank"}.  
Android and iOS however both have their own date pickers build into the OS which is shown when the user taps a native HTM date input.
As these pickers are specifially tailored to touch input and have a UI consistent with current OS, unless you have need certain features only provided by a particular plugin, in many cases this will be the preferred method for mobile.
</p>

Continuing on from the [first part]({% post_url 2020-07-17-flexbox-basics %}) where we talked about flexbox container properties, in this post we'll take a look at properties that can be applied to the flex items within those containers.
As a quick reminder, flex items are all elements that are the direct children of a flex container (an element with `display: flex`).<br/>

### flex-grow

When there is more space in the flex container than is needed to display all items along the main axis, `flex-grow` defines how much an element can grow in size. Both `flex-grow` and `flex-shrink` are relative values, meaning the effect they have is determined by the ratio of the value to other elements.
For example in the following layout, item 2 would have a width of double each of the other elements as `2` is double the size of `1`.

| item-1         | item-2         | item-3         |
| -------------- | -------------- | -------------- |
| `flex-grow: 1` | `flex-grow: 2` | `flex-grow: 1` |

<div style="display: flex; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;margin-right: 2px;flex-grow: 1;">Item 1</div>
  <div style="background-color: #223344;color: white;flex-grow: 2;">Item 2</div>
  <div style="background-color: #223344;color: white;margin-left: 2px;flex-grow: 1;">Item 3</div>
</div><br/>

The default value for `flex-grow` is `0`, meaning this element is not allowed to grow at all and uses up only enough space as is necessary.<br/>

### flex-shrink

In a similar way to `flex-grow`, when there is not enough space to display all items along the main axis, `flex-shrink` defines how much each element can shrink.
Let's look at a simple example.

| container      | item-1                          | item-2                          | item-3                          |
| -------------- | ------------------------------- | ------------------------------- | ------------------------------- |
| `width: 500px` | `flex-shrink: 0; width: 200px;` | `flex-shrink: 1; width: 200px;` | `flex-shrink: 0; width: 200px;` |

<div style="display: flex; width: 500px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;margin-right: 2px;flex-shrink: 0;width: 200px;">Item 1</div>
  <div style="background-color: #223344;color: white;flex-shrink: 1;width: 200px;">Item 2</div>
  <div style="background-color: #223344;color: white;margin-left: 2px;flex-shrink: 0;width: 200px;">Item 3</div>
</div><br/>

With items 1 and 3 having a `flex-shrink` of `0`, meaning they cannot shrink, their width remains at the specified `200px`.
Item 2 on the other hand with a `flex-shrink` of `1`, and so shrinks to the width of the available remaining space, or `100px`.

The default value of `flex-shrink` is `1`, and like `flex-grow`, `flex-shrink` is relative so specifying values greater than 0 for multiple elements will cause them to shrink proportionally.

| container      | item-1                          | item-2                          |
| -------------- | ------------------------------- | ------------------------------- |
| `width: 200px` | `flex-shrink: 2; width: 200px;` | `flex-shrink: 1; width: 200px;` |

<div style="display: flex; width: 200px;padding: 5px; background-color: #f2f2f2f2;">
  <div style="background-color: #223344;color: white;margin-right: 2px;flex-shrink: 2;width: 200px;">Item 1</div>
  <div style="background-color: #223344;color: white;flex-shrink: 1;width: 200px;">Item 2</div>
</div><br/>

Here the total width of items is 400px, but the container is only `200px` width. Since `flex-shrink` is greater than `0` on both items, they both shrink.
And because item 1 has a `flex-shrink` value double that of item 2, item 1 shrinks twice as much as item 2.<br/>

### flex-basis

`flex-basis` simply defines the initial size (before any growing or shrinking) for a flex item along the main axis and is basically equivalent to the standard `width` (for row layouts) or `height` (for column layouts) property.
Its default value, as with `width` and `height`, is `auto`.<br/>

### flex

Having introduced the `flex-grow`, `flex-shrink`, and `flex-basis` properties, I'm sorry to have to tell you that in general you shouldn't actually use them!
That's not to say you shouldn't use the actual properties themselves, but for conciseness the best practice is to specify them using the `flex` property as follows:

`flex: <flex-grow> <flex-shrink> <flex-basis>`

Remembering our default values for each individual property we can write the default `flex` of a flex item as `flex: 0 1 auto`.<br/>

### align-self

If you remember back to our discussion of [flex container properties]({% post_url 2020-07-17-flexbox-basics %}), the `align-items` container property sets the alignment of items along the cross axis.
`align-self` is used when you want to specify a different alignment for a single element.

Here is an example where a `flex-direction: row` container has an `align-items` value of `flex-start`, aligning items to the top of the cross (vertical) axis.  
Item 3 has an `align-self` value of `flex-end`, causing it to be aligned to the bottom instead.

<div style="display: flex; width: 500px; height: 50px; padding: 5px; justify-content: space-evenly; background-color: #f2f2f2f2; align-items: flex-start;">
  <div style="background-color: #223344;color: white;width: 100px; height: 20px; ">Item 1</div>
  <div style="background-color: #223344;color: white;width: 100px;height: 20px; ">Item 2</div>
  <div style="background-color: #223344;color: white;width: 100px;height: 20px; align-self: flex-end; ">Item 3</div>
</div><br/>

### order

The final flex item property we will look at is `order`, which allows you to change the order of items to something other than the order they are specified in the source.  
`order` has a default value of `0` and items are arraged in order of their `order` values, with items with the same `order` being displayed in the order they appear in the source.

To reverse the order of items in the previous example, we could set the `order` of item 3 to `1`, item 2 to `2`, and item 1 to `3`.  
(In this case it would be simpler to just set the `flex-direction` to `row-reverse` to achieve the same effect.)

<div style="display: flex; width: 500px; height: 50px; padding: 5px; justify-content: space-evenly; background-color: #f2f2f2f2; align-items: flex-start;">
  <div style="background-color: #223344;color: white;width: 100px; height: 20px; order: 3; ">Item 1</div>
  <div style="background-color: #223344;color: white;width: 100px;height: 20px; order: 2;">Item 2</div>
  <div style="background-color: #223344;color: white;width: 100px;height: 20px; align-self: flex-end; order: 1;">Item 3</div>
</div><br/>

Note that because `order` causes items to be displayed on screen in a different order than they exist in the source, care must be taken not to sacrifice accessibility for keyboard and screen reader users.<br/>

That just about covers the basics of flexbox, for more information on some of the quirks or less common properties of CSS flexbox I encourage you to take a look at the [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout){:target="\_blank"}.

{% include share-buttons.html %}
