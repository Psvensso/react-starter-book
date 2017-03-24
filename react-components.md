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



