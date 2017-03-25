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

##### 

##### setState

When a setState function is called on a component React will create a new element tree from that node down and do a reconciliation against previous version of the tree and current. Since this happens with plain javascript object this is sometimes referred to the as "virtual DOM".

By the end of the reconciliation, React knows the result DOM tree, and a renderer  applies the minimal set of changes necessary to update the DOM nodes \(or the platform-specific views in case of React Native\).

##### shouldComponentUpdate

When React does its "tree diff" and calls every tree node to compare you can hook into that compare using a lifecycle method called `shouldComponentUpdate:()=>boolean`.  ShouldComponentUpdate makes it possible for us to say "stop processing this sub-tree. nothing has changed here", React skips the node and its children and continues elsewhere.

[More from the documentation](https://facebook.github.io/react/docs/optimizing-performance.html#shouldcomponentupdate-in-action)

