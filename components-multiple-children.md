# Components - Multiple children

One common scenario is to return multiple children from a component. This would be the case for a list or a grid for example.   
Let's look at some JSX trickery that uses javascripts buildt-in mapping features. 

```
interface ICustomer {
    name: string;
    company: string;
}

interface ICustomerTableProps {
    customers: ICustomer[]
}

export class CustomerTable extends React.Component<ICustomerTableProps, any>{
    render() {
        const customers = this.props.customers;
        return <table>
            {//Inside JS
                customers.map((customer, index) => <tr>
                    <td>{customer.name}</td>
                    <td>{customer.company}</td>
                </tr>)
            }
        </table>;
    }
}
const fakeCustomers = [
    {
        name: "Per",
        company: "Webstep"
    }, 
    {
        name: "John",
        company: "Microsoft"
    }
];

//Usage 
render(
    <CustomerTable customers={fakeCustomers} />,
    document.getElementById("app")
);
```

Can you use this with other mapping functions like filter or reduce?

Let's write a component that filters.

```
 export class MicrosoftTable extends React.Component<ICustomerTableProps, any>{
    render() {
        const customers = this.props.customers;
        return <table>
            {
                customers
                .filter(x => x.company === "Microsoft")
                .map((customer, index) => <tr>
                    <td>{customer.name}</td>
                    <td>{customer.company}</td>
                </tr>)
            }
        </table>;
    }
}
```

How can we write this more pretty?  .... or is it already pretty damn pretty.





