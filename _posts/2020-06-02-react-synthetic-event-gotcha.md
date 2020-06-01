---
layout: post
title: 'React SyntheticEvent gotcha'
date: 2020-06-02 00:26:00 +0900
categories: react events
---

If you know about React's synthetic events already this will be an easy one, if not take a look at the following (simplified) functional component and see if you can spot the bug.

## The Problem

The form below contains two checkboxes. Checking a checkbox should set the property of formData that matches its name to its checked value.

```javascript
const [formData, setFormData] = React.useState({
  checkOne: false,
  checkTwo: false
});

const onClick = (e) => {
  setFormData(prevFormData => {
    return {
      ...prevFormData,
      [e.target.name]: e.target.checked
    }
  });
}

return {
  <form>
    <input type="checkbox" value={formData.checkOne}
        name="checkOne" onClick={onClick} /> Check One
    <input type="checkbox" value={formData.checkTwo}
        name="checkTwo" onClick={onClick} /> Check Two
  </form>
}
```

I came across this myself today in a form and it took a couple of minutes to realize what the issue was. For some reason I was getting an error that `e.target.name` and `e.target.checked` could not be found as `e.target` was `null`.

The problem here is that for performance reasons, React does not pass onclick events, onchange events, and other user events directly to your event handlers, but rather wraps them, converting them to **Synthetic events**.

Now while in most cases these synthetic events can be treated the same as raw events, React actually **reuses** them, setting their properties (including target) to **null** after the event handler has run. Now can you see the issue with the above code?

Because the new state of formData depends on its previous state, we need to pass a function to the setFormData setter to ensure consistency. This function however is executed after the onClick event handler returns, by which point React has already set the `target` property of the synthetic event object to null.

## The Solution

Once you realize this, the fix is quite simply to cache the values you need to use.

```javascript
setFormData((prevFormData) => {
  const { name, checked } = e.target;
  return {
    ...prevFormData,
    [name]: checked,
  };
});
```

Easy to avoid once you know.

For more information on synthetic events, checkout the relevant pages of the [React docs](https://reactjs.org/docs/events.html).

{% include share-buttons.html %}
