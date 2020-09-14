---
layout: post
title: "Avoiding useSelector unnecessary rerenders"
date: 2020-09-14 23:26:00 +0900
categories: react redux performance
---

Making the switch from class based components to functional components with hooks is well worth it, but some care must be taken as well.
One such instance came up when converting an existing redux connected class component to the redux `useSelector` hook.

## The Problem

I noticed that when typing text in an input in one area of the application, the entire application would rerender, making typing painfully laggy and slow.
After investigating the renders and unsuccessfully trying to React.memoize related components, I discovered the issue was with my use of the `useSelector` hook.
Look at the following example of `useSelector` and see if you can spot the issue.

```javascript
const [value1, value2] = React.useSelector((state) => [
  state.value1,
  state.value2,
]);
```

To find and fix the problem, we first need to understand that changes to the app state returned from a `useSelector` hook will trigger a rerender of the component.
By default, useSelector use strict === equals to determine if state has changed. You may see now that we are creating a new array containing `value1` and `value2` _every single time_, and since two different arrays can never be strictly equal, this means that the component will rerender _every single time_.

## Solution 1 - Seperate useSelector calls

One solution, assuming that `value1` and `value2` are either primitive or immutable values, would be separate the two values we retrieve from the state into two seperate `useSelector` calls.

```javascript
const value1 = React.useSelector((state) => state.value1);
const value2 = React.useSelector((state) => state.value2);
```

Since we are returning the value itself from each `useSelector` call, if the value is primitive such as a number or string, or an immutable object that is set to a different reference when changes are made, we can safely trust that strict === equality will be able to tell us whether the previous and next values are the same or not.

## Solution 2 - Define an equality function

Another solution, is to specify a custom equality function for `useSelector` to use to determine if the previous and next returned values are identical or not.
`react-redux` exports a shallow equality function that can be used which as you may expect performs a shallow equality comparison to determine if a rerender is necessary.

```javascript
const [value1, value2] = React.useSelector(
  (state) => [state.value1, state.value2],
  shallowEqual
);
```

If this does not suit your needs, you can of course supply your own equality function and completely customize how you determine if two returned states are different and require a rerender, or not.

For more information on `useSelector` check out the relevant pages of the [React docs](https://react-redux.js.org/7.1/api/hooks#useselector){:target="\_blank"}.

{% include share-buttons.html %}
