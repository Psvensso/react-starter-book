# What is React

React is a [open-source javascript](https://github.com/facebook/react) library developed and maintained by Facebook. With React you create UI views and depending on who´s rendering you output the view tree into your device of choice, this can be the DOM if you are using the `react-dom` package or a mobile phone if using the `react-native` package. That was a cryptic explanation but so is React in some ways. Lets try to clean the picture by first declaring what it's not.

* ### React is NOT a component library
* ### React does NOT contain any service injection or other bootstrapping of files
* ### React does NOT contain any router
* ### React does NOT have a template system
* ### React does NOT implement the MV\*\* pattern

With that in mind let's first look what we are trying to solve by defining some paradigms.  
Let's look at the MVC/MV\* pattern.

### Recap MV\*

In an interactive application the hard part is to manage state. The well proven and long lived MVC trickery works as follows.

![](https://upload.wikimedia.org/wikipedia/commons/9/9d/MVC-basic.svg)

MVC proposes that the model is the single source of truth, all state lives in the model. Views are derived from the model and must be kept in sync, when the model updates so must the view. State changes are done via the controller that updates the view.

So on a "UML"-type of level this is a quite simple pattern that promises to:

> The MVC design pattern decouples these major components allowing for efficient code reuse and parallel development.

This looks quite simple. First, we need to describe our View using HTML for example and how it transforms the model into the DOM. Then, whenever the user acts we update the model and re-render the entire thing. Unfortunately, this is not very straightforward.

The first problem is that the DOM naturally comes with some state binding capabilities such as user data input so we can not just re-render the entire thing and the second major problem is that rendering DOM elements are **really slow**.

So what do we do, how do we keep the model in sync with our view/DOM?

#### Data binding

For the past 4 years, the most common framework feature introduced to solve this problem was data binding.

Data binding is the ability to keep your model and view in sync automatically. Usually that means your JavaScript objects and your DOM.

It achieves that by letting you declare the dependencies between the pieces of data in your app and changes in the state are propagated throughout your application and all depending pieces are "automagically" updated.

#### Knockout

Knockout argues for the [**MVVM**\(Model-View-ViewModel\)](http://knockoutjs.com/documentation/observables.html) approach and helps you implement the “View” parts

[Fiddle kncockout example](https://jsfiddle.net/fgrk1ps3/1/)  

