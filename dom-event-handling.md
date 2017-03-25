# DOM Event handling

To make your UI reactive something needs to trigger the change. This is most likely an event comming from the user interacting with the DOM. React handles all DOM events for you so you can only focus on your components. In this chapter we look at how to wire up event handlers on your components.

##### Attaching event handlers

Adding event handlers to a React component is very similar to attaching a handler on a regular DOM node.

Vanilla JS:

```
<button onclick="console.log('The link was clicked.'); return false">
  Click me
</button>
```

TSX TypeScript React:

```
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

Note the difference in how the event names are different, React always camelCases their event names.  
_Can you find the event available on a JSX &lt;form&gt; element? \(tip: F12 in VSCode\) _

---

Exercise: The tab bar, setting local state and handling click events 

---





