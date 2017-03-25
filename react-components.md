# React Components, Elements, and Instances

---

**Note!**  
_Big chunks of this page is taken from the React team´s _[_excellent blog_](https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html)_.  
Go and check it out when you have a spare moment._

_Some of this code is pseudo code and wont actually run or compile with Typescript,  
read the footnotes before testing out any code examples._

---

The end result of rendering a React component is a element. In React you can write raw elements or more common write components that when they run returns elements or trees of elements.

---

In React a element is a plain object describing a component instance or DOM node and its desired properties.

An element is not an actual instance. Rather, it is a way to tell React what you want to see on the screen.  
You can’t call any methods on the element.

```
 //TypeScript interface of a ReactElement

 interface ReactElement<P> {
        type: string | ComponentClass<P> | SFC<P>;
        props: P;
        key: string | number | null;
 }

 //Example In JSON Form
 {
   key: 0,
   type: 'button',
   props: {}
 }
```

---

####  {#thebutton}

#### The Button element example {#thebutton}

When an element’s`type`is a string, it represents a DOM node with that tag name, and`props`correspond to its attributes.  
This is what a React component will render. For example:

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
//HTML representation
<button class='button button-blue'>
  <b>
    OK!
  </b>
</button>
```

Note how elements can be nested. By convention, when we want to create an **element tree**, we specify one or more child elements as the`children`prop of their containing element.

What’s important is that both child and parent elements are _just descriptions and not the actual instances_.

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
    },
    {
      type: Button,
      props: {
        color: 'blue',
        children: 'Cancel'
      }
   }]
}
```

Or, if you prefer JSX \(and we do\):

```
(
  <div>
    <p>Are you sure?</p>
    <Button color='blue'>Cancel</Button>
  </div>
)
```

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
interface IPropInterface {
    color: string;
    text: string
}

interface IState {

}


// 1) As a function of props
const CancelButton = ({ color, text }:IPropInterface) => (
    <button color={color}>{text}</button>
);

// 2) Using the React.createClass() factory
const OkButton = React.createClass<IPropInterface, IState>({
    render() {
        const { color, text } = this.props;
        return <button color={color}>{text}</button>;
    }
});

// 3) As an ES6 class descending from React.Component and state
class SubmitButton extends React.Component<IPropInterface, IState> {
    render() {
        const { color, text } = this.props;
        return <button color={color}>{text}</button>;
    }
}
```

A functional component is less powerful but is simpler, and acts like a class component with just a single render\(\) method. Unless you need features available only in a class, we encourage you to use functional components instead.

**However, whether functions or classes, fundamentally they are all components to React. They take the props as their input, and return the elements as their output.**

**Mindset**: A react component is an idempotent function that returns a element or another component.

![](/assets/propertiesToElement.png)

---

Exercise time!

---

# Component properties

As you saw in the earlier component examples the component function take in a set or read-only arguments. The arguments are called props in the React universe.

The read-only part is important as it makes the functions "pure". Meaning that it does not change their own input and given the same input they return the same result.

```
interface IProperties{
    name:string;
    fontSize: number;
}

export const MyPureComponent = function(props:Readonly<IProperties>){
    props.name = "Ok";
    return <div>
        {JSON.stringify(props)}
    </div>;
}
```

A bad un-pure example:

```
interface IProperties{
    person: {name: string};
}

export const MyPureComponent = function(props:IProperties){
    props.person.name = "John";
    return <div>
        {JSON.stringify(props)}
    </div>;
}
```

When we create a component class React will make sure that our properties are read only and will throw an error if you try to re assign them. Don't confuse this with immutability, we come to that later, for now just note down that you can't and should not change a property.

---

Exercise

Remember that we said about if an element’s`type`is a string, it represents a DOM node with that tag name, and`props`correspond to its attributes. Let's look at some JSX and try to figure out what props we can pass down to them.

What properties can we pass down to a &lt;div&gt; component? \(tip: F12 in visual studio code\)

---

```
//Passing and transforming props example
interface IMyListProps {
    fontSize:number; 
    color: string;
};

export class MyList extends React.Component<IMyListProps, void>{
    public static defaultProps:IMyListProps = {
        fontSize: 12,
        color: "blue"
    }

    render(){
        return <div style={this.props}>How do i look?</div>;
    }
}
```

_Can you change this so that you can send in the text "How do i look?_" as well?

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

Runnable example of rendering an raw json element:

```js
import * as React from "react";
import { render } from "react-dom";

render({
    "$$typeof": Symbol.for('react.element'),
    key: null,
    type: 'div',
    props: {
        className: "main container-fluid",
        children: "Hello world!"
    }
} as any,
    document.getElementById("app")
);
```



