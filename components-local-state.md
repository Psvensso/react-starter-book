# Component state adn lifecycle

So far we have only learned one way to update the actual UI. We call`ReactDOM.render()`to apply the rendered output to the browser DOM. `ReactDOM.render()` method does what React calls an initial render and build up that tree of elements they call the "virtual dom". Look at this bad example on updates from the [React documentation](https://facebook.github.io/react/docs/state-and-lifecycle.html).

```
function tick() {

  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );

  ReactDOM.render(
    element,
    document.getElementById('app')
  );

}

setInterval(tick, 1000);
```

Next, let's look at how a component can "update" itself and handle som lifecycle hooks without creating an entire new tree.

React component \(only components, not stateless functions\) can hold something we call state. Let's take out example from above and convert it into a component first.

```
export class StaticClock extends React.Component<IClockProps, IClockState>{
    constructor(props) {
        super(props);
        //We set the default state in the contructor
        this.state = {
            time: new Date()
        };
    }

    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.state.time.toLocaleTimeString()}.</h2>
            </div>
        );
    }
}
```

  
Now we are getting close to something that looks as a model. And yes, the state and props can be looked at as the model but there is no binding going on. Were only rendering what we see and we don't update "the model" here.

Next we would like to update our state in a setInterval loop. The constructor is all about bootstrapping static content like state but for this we need to look at React´s lifecycle. 



**Lifecycle hooks**

A React component goes through a set of lifecycles and we can set callback to be notified by them.  
The interface for a lifecycle component looks like this in TypeScript.

```
interface ComponentLifecycle<P, S> {
        componentWillMount?(): void;
        componentDidMount?(): void;
        componentWillReceiveProps?(nextProps: Readonly<P>, nextContext: any): void;
        shouldComponentUpdate?(nextProps: Readonly<P>, nextState: Readonly<S>, nextContext: any): boolean;
        componentWillUpdate?(nextProps: Readonly<P>, nextState: Readonly<S>, nextContext: any): void;
        componentDidUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>, prevContext: any): void;
        componentWillUnmount?(): void;
}
```

Can you find this interface in your editor? \(Tip: F12 React.Component, F12 ComponentLifecycle\)

  
The lifecycle is build up in three steps:

Birth, life, death.

Birth - happens at the initial rendering of the component.   
Life - Where the component waits and possibly re-renders.  
Death - Called before removed from the DOM.

##### ![](/assets/lifecycle.png)







