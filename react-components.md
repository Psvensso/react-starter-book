# React Components, Elements, and Instances

---

**Note!**  
_Big chunks of this page is taken from the React team´s _[_excellent blog_](https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html)_.  
Go and check it out when you have a spare moment._

_Some of this code is pseudo code and wont actually run or compile with Typescript,  
read the footnotes before testing out any code examples._

---

The difference between **components, their instances, and elements **confuses many React beginners. Why are there three different terms to refer to something that is painted on screen? Let's break it down.

In React \(when targeting the web\) a element is a plain object describing a component instance or DOM node and its desired properties.

An element is not an actual instance. Rather, it is a way to tell React what you want to see on the screen. You can’t call any methods on the element. It’s just an immutable description object with two fields: type: \(string \| ReactClass\) and props: Object.

####  {#thebutton}

####  {#thebutton}

####  {#thebutton}

#### The Button {#thebutton}

When an element’s`type`is a string, it represents a DOM node  \(or a native view component when developing with react native\) with that tag name, and`props`correspond to its attributes. This is what React will render. For example:

```
//An "element"
{
  type: 'button',
  props: {
    className: 'button button-blue',
    children: {
      type: 'b',
      props: {
        children: 'OK!'
      }
    }
  }
}
```

This element is just a way to represent the following HTML as a plain object:

```
<button class='button button-blue'>
  <b>
    OK!
  </b>
</button>
```

Note how elements can be nested. By convention, when we want to create an **element tree**, we specify one or more child elements as the`children`prop of their containing element.

What’s important is that both child and parent elements are _just descriptions and not the actual instances_.

--An element is not attached to the DOM in any way.

### Component Elements

However, the`type`of an element can also be a function or a class corresponding to a React component:

```
{
  type: Button,
  props: {
    color: 'blue',
    children: 'OK!'
  }
}
```

This is the core idea of React.

An element describing a component is also an element, just like an element describing the DOM node. They can be nested and mixed with each other.

You can mix and match DOM and component elements in a single element tree:

```
{
  type: 'div',
  props: {
    children: [{
      type: 'p',
      props: {
        children: 'Are you sure?'
      }
    }, {
      type: DangerButton,
      props: {
        children: 'Yep'
      }
    }, {
      type: Button,
      props: {
        color: 'blue',
        children: 'Cancel'
      }
   }]
}
```

Or, if you prefer JSX:

```
(
  <div>
    <p>Are you sure?</p>
    <DangerButton>Yep</DangerButton>
    <Button color='blue'>Cancel</Button>
  </div>
)
```

### 

### 

### 

### Components Encapsulate Element Trees

When React sees an element with a function or class type, it knows to ask that component what element it renders to, given the corresponding props.

When it sees this element:

```
{
  type: Button,
  props: {
    color: 'blue',
    children: 'OK!'
  }
}
```

React will ask Button what it renders to. The Button will return this **element**:

```
{
  type: 'button',
  props: {
    className: 'button button-blue',
    children: {
      type: 'b',
      props: {
        children: 'OK!'
      }
    }
  }
}
```

React will repeat this process until it knows the underlying DOM tag elements for every component on the page.

**The returned element tree can contain both elements describing DOM nodes, and elements describing other components. This lets you compose independent parts of UI without relying on their internal DOM structure.**

### 

### 

### 

### Components Can Be Classes or Functions

For a React component, props are the input, and an element tree is the output.

In the code above Button are a React component. It can either be written as functions, like above, or as a class descending from React.Component. These three ways to declare a component are mostly equivalent:

```
// 1) As a function of props
const Button = ({ children, color }) => ({
  type: 'button',
  props: {
    className: 'button button-' + color,
    children: {
      type: 'b',
      props: {
        children: children
      }
    }
  }
});

// 2) Using the React.createClass() factory
const Button = React.createClass({
  render() {
    const { children, color } = this.props;
    return {
      type: 'button',
      props: {
        className: 'button button-' + color,
        children: {
          type: 'b',
          props: {
            children: children
          }
        }
      }
    };
  }
});

// 3) As an ES6 class descending from React.Component
class Button extends React.Component {
  render() {
    const { children, color } = this.props;
    return {
      type: 'button',
      props: {
        className: 'button button-' + color,
        children: {
          type: 'b',
          props: {
            children: children
          }
        }
      }
    };
  }
}
```

A functional component is less powerful but is simpler, and acts like a class component with just a single render\(\) method. Unless you need features available only in a class, we encourage you to use functional components instead.

**However, whether functions or classes, fundamentally they are all components to React. They take the props as their input, and return the elements as their output.**

**Mindset**: A react component is a idempotent function that returns a element or another component.

### Top-Down Reconciliation

When you call:

```
ReactDOM.render({
  key: 0,
  type: Form,
  props: {
    isSubmitted: false,
    buttonText: 'OK!'
  }
}, document.getElementById('root'));
```

React will ask the Form component what element tree it returns, given those props. It will gradually “refine” its understanding of your component tree in terms of simpler primitives:

```
// React: You told me this...
{
  type: Form,
  props: {
    isSubmitted: false,
    buttonText: 'OK!'
  }
}

// React: ...And Form told me this...
{
  type: Button,
  props: {
    children: 'OK!',
    color: 'blue'
  }
}

// React: ...and Button told me this! I guess I'm done.
{
  type: 'button',
  props: {
    className: 'button button-blue',
    children: {
      type: 'b',
      props: {
        children: 'OK!'
      }
    }
  }
}
```

This is a part of the process that React calls reconciliation which starts when you call ReactDOM.render\(\) or setState\(\). By the end of the reconciliation, React knows the result DOM tree, and a renderer like react-dom or react-native applies the minimal set of changes necessary to update the DOM nodes \(or the platform-specific views in case of React Native\).

This gradual refining process is also the reason React apps are easy to optimize. If some parts of your component tree become too large for React to visit efficiently, you can tell it to skip this “refining” and diffing certain parts of the tree if the relevant props have not changed. It is very fast to calculate whether the props have changed if they are immutable, so React and immutability work great together, and can provide great optimizations with the minimal effort.

React takes care of creating an instance for every class component, so you can write components in an object-oriented way with methods and local state, but other than that, instances are not very important in the React’s programming model and are managed by React itself.

# Summary

An element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components. Elements can contain other elements in their props. Creating a React element is cheap. Once an element is created, it is never mutated.

A component can be declared in several different ways. It can be a class with a render\(\) method. Alternatively, in simple cases, it can be defined as a function. In either case, it takes props as an input, and returns an element tree as the output.

When a component receives some props as an input, it is because a particular parent component returned an element with its type and these props. This is why people say that the props flows one way in React: from parents to children.

An instance is what you refer to as this in the component class you write. It is useful for storing local state and reacting to the lifecycle events.

Functional components don’t have instances at all. Class components have instances, but you never need to create a component instance directly—React takes care of this.

**Finally, to create elements, use React.createElement\(\), JSX, or an element factory helper. Don’t write elements as plain objects in the real code—just know that they are plain objects under the hood.**









---

Footnote:

All React elements require an additional`$$typeof: Symbol.for('react.element')`field declared on the object for [security reasons](https://github.com/facebook/react/pull/4832).  
It is omitted in the examples above. The examples above uses inline objects for elements to give you an idea of what’s happening underneath but the **code won’t run as is** unless you either add `$$typeof`to the elements, or change the code to use`React.createElement()`or JSX.

Also the TypeScript interface does not include the `$$typeof` property so we must cast the object type to any.

Runnable example:

```js
import * as React from "react";
import { render } from "react-dom";
const el = React.createElement("", );
render({
    "$$typeof": Symbol.for('react.element'),
    key: null,
    type: 'div',
    props: {
        className:"main container-fluid",
        children: "Hello world!"
    }
} as any,
    document.getElementById("app")
);
```

We will not use this syntax anymore in the chapters that follows. This is only to understand the underlying process. We will mainly use JSX. 

---

Now let's go and look at immutability and why it's so important to the React ecosystem.

