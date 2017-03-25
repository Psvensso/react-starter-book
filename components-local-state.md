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





