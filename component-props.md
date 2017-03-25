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

_Can you change this so that you can send in the text instead?_









