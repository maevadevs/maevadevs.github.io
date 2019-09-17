---
layout: post
title: Using `refs` With React
category: React
tags: [react, refs]
---

This a short explanation of the usage of `refs` in React.

---

## When to Use Refs

There are a few good use cases for refs:

- Managing focus, text selection, or media playback
- Triggering imperative animations
- Integrating with third-party DOM libraries

## Creating Refs

- Refs are created using `React.createRef()`
- Created refs are attached to React elements via the `ref` attribute
- Refs are commonly assigned to an instance property when a component is constructed
  - This way, they can be referenced throughout the component

{% highlight js %}
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myDivRef = React.createRef();
  }
  render() {
    return <div ref={this.myDivRef} />;
  }
}
{% endhighlight %}

## Accessing a Reference to Node of the Ref

- A reference to the node attached to the ref can be accessed with `.current`
  - For HTML element, returns the DOM node
  - For class component, returns the instance object (don't use on functional components.)

{% highlight js %}
const divNode = this.myDivRef.current;
{% endhighlight %}
