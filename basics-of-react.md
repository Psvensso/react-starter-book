### Compare with other libraries

Before we dig into React lets first try to identify some common problems that older frameworks had and how they solved them and then we look at how React handles the problems.

Most older javascript frameworks implements some sort of MV\* pattern, so time for a small re-cap.

### Re-cap MV\*

In an interactive application the hard part is to manage state. The well proven and long lived MVC pattern is illustrated as follows.

![](/assets/mvc.png)

MVC proposes that the model is the single source of truth, all state lives in the model. Views are derived from the model and must be kept in sync, when the model updates so must the view. State changes are done via the controller that updates the view.

So on a "UML"-type of level this is a quite simple pattern that promises to:

> The MVC design pattern decouples these major components allowing for efficient code reuse and parallel development.



This looks quite simple.  
First, we need to describe our View using HTML or some sort of template and how it transforms the model into the DOM.  
Then, whenever the user acts we update the model and re-render the view. Unfortunately, this is not very straightforward.

The first problem is that the DOM naturally comes with some state binding capabilities such as user data input so we can not just re-render the entire thing or we might loose some of that data. The second major problem is that rendering DOM elements are **really slow**.

![](/assets/dom.png)

So what do we do, how do we keep the model in sync with our view/DOM?

#### 

#### Data binding

For the past 4 years, the most common framework feature introduced to solve this problem was data binding.

Data binding is the ability to keep your model and view in sync automatically. Usually that means your JavaScript objects and your DOM.

It achieves that by letting you declare the dependencies between the pieces of data in your app and changes in the state are propagated throughout your application and all depending pieces are "automagically" updated.







#### Knockout

Knockout argues for the [**MVVM**\(Model-View-ViewModel\)](http://knockoutjs.com/documentation/observables.html) approach.  
But what about the model being the single source of truth?  
Where should this ViewModel get its state from?  
How does it does it keep in sync with the model?

[Fiddle knockout example](https://jsfiddle.net/Swensson/fgrk1ps3/2/)

#### Angular \(1.5\)

Good old angular tries to keep the model and view in sync using their two way databinding strategy.  
This image is from the Angular documentation.

![](/assets/angular.png)

But is the model really a model here, who owns the state once it morphs and changes over time?  
Perhaps it's more of a viewmodel if the actual model lives else where or a controller behaving like a model?

[Angular example](https://jsfiddle.net/Swensson/h9zuefbc/1/#fontColor=00FF00&type=frame&height=300)

Two way databinding is not rocket science in small application but reasoning around code when "everything can change everything" -- e.g. the view can update the model and the model can update the view becomes harder as the application scales.   
  
This triggers that that changes this that updates that, who owns the data?   
What's the real state?  
  


---

  
These are some of the problems with traditional data binding especially when data changes over time.   
Before we dig into how React solves this lets go and see how we declare and build React components and we'll look at dataflows in a later chapter. 

---

  


#### View and templates

With the MV\* patterns in mind, what is the real difference between your view and your viewmodel in the examples above?   
They both can transform the way they display the data and they both can updates the data.



The view \(DOM nodes\) is often written in a template language like handlebars or html,  
advocates of the "template" paradigm can be fierce defenders of this old saying "don´t mix logic with your views". 

But are the templates not logic, are you controllers or viewModels not transforming the look of the data?

```
{{# each}} 
ng-repeat
databind=”foreach”
value.bind="likesTacos"
```

```
<div *ngFor="let hero of heroes">{{hero.name}}</div>
<input #heroInput> {{heroInput.value}}
```



---

> Templates separate technologies, not concerns

--Pete Hunt, former React core member

---





In React the viewModel and the view are the same thing and we merge the concepts, this allows for much more powerfull views \(they are written in JS\) but at some cost in readability. There for the React team created JSX a hybrid language making writing React components more declarative allowing you to write javascript and a xml syntax language that looks like html.

```
//MyButton.jsx
function MyButton(){
    var shadowSize = 2;
    return <MyButton color="blue" shadowSize={shadowSize }>
          Click Me
    </MyButton>
    
}

```



Note!  
TypeScript has created a Typed version of JSX called TSX. 







