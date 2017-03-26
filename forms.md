# Forms

###### PlayAlong@[005-Forms](https://github.com/Psvensso/react-starter/blob/example-components/Scripts/Examples/Components/005-Forms.tsx)

Remember when we did our [MV\* re-cap](/basics-of-react.md) and how the DOM naturally keeps some state in the DOM. That's why React treats form elements a little bit differently. First lets look at the input element.

There are two "types" of React input elements.

##### Uncontrolled components

Well an uncontrolled component is actually just a normal component that holds its own state in the DOM. React will not replace the component in the DOM upon re-rendering so the state will be in "DOM only" mode. This is generally a bad practise in React and only recommended if you are doing some trickery or custom UI components.

Uncontrolled input:

```
<input type="text" name="name" />
```

_Test it out, can you enter data into the input?  
Can you place a input next to a ticking clock \(earlier example\) and still update the input even though React is re-rendering at intervals?_

##### Controller components

With a controlled  component we want no state to be left in the DOM. The big difference is that react will then replace the value of your component upon re-rendering so you must hold the state and handle state changes.

All you need to create a controlled component is to add the value property. This tells React that you want to be in charge of the state. React then also forces you with a runtime check that you also have a onChange event.[^1]

```
<input type="text" value={this.state.email} onChange={event=>this.setState({email: event.target.value})} />
```

Look at the examples comparing the two forms @ [005-Forms](https://github.com/Psvensso/react-starter/blob/example-components/Scripts/Examples/Components/005-Forms.tsx)











[^1]: There are deviations, for example, on the checkbox you need a checked property instead of value and you can have a controlled value on a input element without a onChange if you have a read-only property as well. **Read up on each type of input element.**

