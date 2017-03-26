### Top-Down Reconciliation

When you call:

```
ReactDOM.render(<div><p>Hello world</p></div>, document.getElementById('root'));
```

React will ask the div component what element tree it returns, given those props. It will gradually “refine” its understanding of your component tree in terms of simpler primitives \(remember that we don´t show key and that $$ property for clarity reasons\):

```
{
    type: 'div',
    props: {
        /**TL;DR; a lot of props*/
        children: function div() {
            return {
                type: 'p',
                props: {
                    /**TL;DR; a lot of props*/
                    children: 'Hello world'
                }
            }
        }
    }
}
```

From this tree of components/elements Reacts creates actual DOM nodes. And a renderer like react-dom or react-native inserts them in the DOM at the given location \(second parameter of ReactDOM.render\). The tree is then stored for later reconciliations.

##### Reacts to setState on this or a higher component

When a setState function is called on a component React will create a new element tree from that node, including all its children, and do a reconciliation against previous version of the tree and current. Since this happens with plain javascript object this is sometimes referred to the as "virtual DOM".

By the end of the reconciliation, React knows the result DOM tree, and a renderer  applies the minimal set of changes necessary to update the DOM nodes \(or the platform-specific views in case of React Native\).

**shouldComponentUpdate**

When React does its "tree diff" and calls every tree node to compare you can hook into that compare using a lifecycle method called `shouldComponentUpdate:()=>boolean`.  ShouldComponentUpdate makes it possible for us to say "stop processing this sub-tree. nothing has changed here", React skips the node and its children and continues elsewhere. More on this in the immutability section.

[More from the documentation](https://facebook.github.io/react/docs/optimizing-performance.html#shouldcomponentupdate-in-action)

**Buzzz: **React is currently working on version 2 of this "compare/diff" algorithm, they call the new React core Fiber. The team has promised that the API should be very close to the same as it is today with a smooth upgrade path. If any breaking changes at all.  
True nerds should look at the super cool talk about [Fiber from React Conf 2017 by Lin Clark](https://youtu.be/S8HXkEnA48g?list=WL&t=6702).

