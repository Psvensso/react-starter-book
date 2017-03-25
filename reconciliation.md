### Top-Down Reconciliation

When you call:

```
ReactDOM.render({
  key: 0,
  type: Button,
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
  type: function Button(){
    return {
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
  },
  props: {
    children: 'OK!',
    color: 'blue'
  }
}





```

From this tree of components Reacts creates actual DOM nodes and inserts them in the DOM at the given location \(second parameter of ReactDOM.render\). The tree is then stored for later reconciliations.

When a setState function is called on a component React will create a new element tree from that node down and do a reconciliation / compare / diff against previous version of the tree and current.

//ToDo... glue.

By the end of the reconciliation, React knows the result DOM tree, and a renderer like react-dom or react-native applies the minimal set of changes necessary to update the DOM nodes \(or the platform-specific views in case of React Native\).

This gradual refining process is also the reason React apps are easy to optimize. If some parts of your component tree become too large for React to visit efficiently, you can tell it to skip this “refining” and diffing certain parts of the tree if the relevant props have not changed. It is very fast to calculate whether the props have changed if they are immutable, so React and immutability work great together, and can provide great optimizations with the minimal effort.

React takes care of creating an instance for every class component, so you can write components in an object-oriented way with methods and local state, but other than that, instances are not very important in the React’s programming model and are managed by React itself.

