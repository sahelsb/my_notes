**React javascript**

First of all we need to install Node.js

We are not gonna use Node.js programming language buut we are gonna use its built\_in tool called node package manager (npm) to install third party libraries in our react app

Then we run this command to install a package that is in npm

npm install -g create-react-app   or    (npm install <create-react-app@1.5.2>)

we are gonna use this package to create a new react app 

Now we use   create-react-app    package to create a new react app using this command -à    create-react-app  my-app

Pay attention : that we create our react app in the folder that we want , so at first we move to the folder that we want and then we create our first react application

![](Aspose.Words.c54aa562-a3fd-44bc-92de-85a129f8d3d3.001.png)Then in order to run this react application we use this command  -à 

cd my-app

npm start

that will lunch our development server in localhost in browser

in the my-app folder, in index.html we have a <div id = root> that is the container for our react application , our App container will start run in this div

then we have react classes like App.js

in classes we return jsx elements  and then this jsx elements are compiled to palin javascript codes that are understandable by browser through babble compiler (babble is the modern javascript compiler)

in our application we need to import objects from modules 

import React from ‘react’;

`	`this is an object	this is a module

const element = <h1> Hello world</h1>     à

this is a react element that is jsx element and it is part of virtual DOM

jsx elements are compiled with babble compiler through calling -à React.create ReactElement()

in the index.js file we render our application using the ReactDOM inside the root element (index.html) then we can see our application inside html page in browser

ReactDom.render(element, document.getElementById(‘root’))

Instead of this element we render our App component in real World application in RecatDom

ReactDom.render(<App/>, document.getElementById(‘root’))

When we want to import modules or classes we use

Import Neighbour from   ./Components/Neighbour

When the two modules are in the same level we just use    ./Neighbour

If we want to go one level up from where the component itself located we use

Import icon form   ./../assets/icon.png

Here   ./   means where the component itself located

We use some shortcuts for convenience, these shortcuts are part of react snippets extension

Imrc : import react

Cc : generate class component

Pay attention: we name our components with capital letters 

Class Counter extends Component

JSX expression must have one parent element : it means in the render method we should always use a div  element and the put all our other elements inside this div

While as we said the jsx elements are compiled with Babbel like this  :   React.createElemenet (name of the element that should be compiled)

State is like an object that contains all the data that the component needs

State = {};

In jsx expressions we can render values dynamically by putting them in {}

<img src = ‘https:….’     -à <img src = {this.state.imageUrl}

For applying attributes to jsx elements we use either classes or styles 

Using <button   ClassName = bootstarp classes

Or

// define style property

Styles = {

// css properties

fontWeight : ‘bold’

};

` `<button   styles = {this.styles}    -à here we should have defined styles property before

OOOOR

Using inline styles

<button  styles = {{fontWeight : ‘bold’}}

Map Method : we use this method to map elements to jsx elements

![](Aspose.Words.c54aa562-a3fd-44bc-92de-85a129f8d3d3.002.png)This.state.neighbours.map(neighbour => <Li  key={neighbour.id}> {neighbour.name}</Li> )}             arrow function

Every item in the list should have a unique key that we passed it here

Conditional rendering :

{ this.state.isShown  && <h1> this is shown </h1>}

Event handling :

button  onClick = {this.handleClick}

Pay attention that here we are not calling the method handleClick (that we should have defined somewhere in the program) buuut we are just giving a reference to tis method therefore we do not use () infront of method name

Binding event handlers :

1\.When we define a method as an event handler we should bind this to the method, otherwise we don not have accees to this and it will be unkhown in the method and so we can not access state properties in the method through this  (current instance of the class)

Depending on how a function is called , this can reference to different objects

So in constructor we should bind the event handlers while in the constructor we have access to this (current object instance of our class) à  

this.handleClick = this.handleClick.bind (this)

2\. another way to do this is defining our function as an arrow function (not when referencing but somewhere else when we define our methods) , if we use arrow function we do not need to bind this anymore

Pay attention , if we have defined a method and we want to call it in jsx expression we use {this.format()} because this is a method call

Updating State :

This.setState({ count : this.state.count <sup>+</sup> 1});

setState() is an asynchronous method , when setState is called the state of the component changes and React will schedule a call to the render method and render the component again (figure out which element has changed and update only that element) somewhere in future (we don not khow when)

passing Argument to event handlers :

we can not pass arguments in the reference to event handler , because as we told it is just a reference not a function call

for this problem we can use arrow functions to pass arguments

<button  onClick = { () => this.handleClick ( id ) }

Props:

Every component has a property called props that is a plain javascript object that has all the propperties that we pass from other componnets

<Neighbour  name = {name} , lable = {lable}>

Now inside the Neighbour component we can use this properties that are passed form outside

This.setState({

neighbourElement : this.props.name;

})

Props is the data that we pass to a component but state is the data that is local and private to that component, state is invisible to other components

Props is read-only à it means that we can not change the properties of props that is passed to a component inside that component

Modifying a state that is inside one component should be done by that component itself

So if we want to modify state of another component (parent) in one component (child) we should raise an event in child component and then parent component handle this event to modify its state (we should implement the event handler in parent component and pass a reference using props to the child component)

Class Parent :

handleSearch = (id) = > {

};

<child  onSearch = {handleSearch} >

In child component :

<button onClick = {  ()=> this.props.onSearch(id) }    -à reference to event handler in parent class

When we want to delete an item from the array in State we use filter method

In the method we want to handle the event :

Const neighbours = this.state.neighbours.filter( n => n.id !== id)

This.setState({

neighbours : neighbours;

});

Controlled components :

It does not have state itself but it just using props that is passed from another componnets and raise events, so it is entirely controlled by its parent, so in this comonents we just delete local state

How to change an state array :


How we can pass props to sibling component :

When we want to share data between sibling components we should lift state up, it means that we dlete the state from child components and put all in parent component then via props we can communicate and sync child components

Stateless functional compoenets: 

When a component does not have any state and and get the data via props then we can change it to functional component

const Navbar = (props) => {

return(

{props.neighbour}

);

};

Lifecycle hooks :

` `they are called in order, and they are only called in class components

when a component is rendered all its children are rendered recursively

![Diagram

Description automatically generated](Aspose.Words.c54aa562-a3fd-44bc-92de-85a129f8d3d3.003.png)

**React render and re-render :**

Rendering describes the process of generating an image.

**DOM** :

"The W3C Document Object Model (**DOM**) is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document."

In plain English, this means that **the DOM represents what you see on your screen** when you open a website, expressed through the markup language HTML.

Browsers allow the JavaScript language to modify the DOM through an API: The globally available document represents that state of the HTML DOM and provides us with functions to modify it.

**VDOM :**

Then we have the Virtual DOM (or VDOM) of React, another abstraction layer on top of that. It consists of your React application's elements.

**State changes in your application will be applied to the VDOM first**. If the new state of the VDOM requires a UI change, the *ReactDOM* library will efficiently do this by trying to update only what *needs* to be updated.For example, if only the attribute of an element changes, React will only update the attribute of the HTML element by calling document.setAttribute.

Updating the VDOM doesn't necessarily trigger an update of the real DOM.

When the VDOM gets updated, React compares it to to a previous *snapshot* of the VDOM and then ***only* updates what has changed in the real DOM**. If nothing changed, the real DOM wouldn't be updated at all. **This process of comparing the old VDOM with the new one is called *diffing***.

Real DOM updates are slow because they cause an actual re-draw of the UI. React makes this more efficient by updating the smallest amount possible in the real DOM.

**Performance :**

When we talk about renders in React, we really talk about the **execution of the render function**, which **doesn't always imply an update of the UI**.

In function components, the execution of the whole function is the equivalent of the render function in class components.

Lets see this example :

![Text

Description automatically generated](Aspose.Words.c54aa562-a3fd-44bc-92de-85a129f8d3d3.004.png)

When the state changes in the parent component (in this case, App), the two Tile components will re-render**, even though the second one doesn't even receive any props.**

This translates to having **the render function being called three times**, but actual DOM modifications only happen once in the Tile component that displays the message

The execution of these render functions has two drawbacks:

1. React has to run its diffing algorithm on each of those components to check whether it should update the UI.
1. All your code in these render functions or function components will be executed again.

**When does react re-render ?**

React *schedules* a render every time the **state of a component** changes.

**Scheduling** a render means that this doesn't happen immediately. React will try to find the best moment for this.

Changing the **state** means that React triggers an update **when we call the setState function (in React hooks, you would use useState**). This doesn't only mean the component's render function will be called, but also that **all its subsequent child components will re-render, regardless of whether their props have changed or not**.

If your application is poorly structured, you might be running a lot more JavaScript than you expected because updating the parent node implies running the render function of **all children**.

As we already saw before, React re-renders a component when you call the setState function to change the state (or the provided function from the useState hook in function components).

As a result, the child components only update when the parent component's state changes **with one of those functions**.

You're looking for componentDidUpdate() which gets triggered after every state or prop change. The componentDidMount() method only runs a single-time.

**The Component lifecycle :**

**Mounting**

These methods are called in the following order when an instance of a component is being created and inserted into the DOM:

- [**constructor()**](https://reactjs.org/docs/react-component.html#constructor)
- [static getDerivedStateFromProps()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
- [**render()**](https://reactjs.org/docs/react-component.html#render)
- [**componentDidMount()**](https://reactjs.org/docs/react-component.html#componentdidmount)

**Updating**

An update can be caused by changes to props or state. These methods are called in the following order when a component is being re-rendered:

- [static getDerivedStateFromProps()](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)
- [shouldComponentUpdate()](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)
- [**render()**](https://reactjs.org/docs/react-component.html#render)
- [getSnapshotBeforeUpdate()](https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)
- [**componentDidUpdate()**](https://reactjs.org/docs/react-component.html#componentdidupdate)




**Unmounting**

This method is called when a component is being removed from the DOM:

- [**componentWillUnmount()**](https://reactjs.org/docs/react-component.html#componentwillunmount)

**lifecycle methods :**

**render() :**

The render() method is the only required method in a class component.

When called, it should examine this.props and this.state and return one of the following types:

- **React elements.** Typically created via [JSX](https://reactjs.org/docs/introducing-jsx.html). For example, <div /> and <MyComponent /> are React elements that instruct React to render a DOM node, or another user-defined component, respectively.
- **Arrays and fragments.** Let you return multiple elements from render. See the documentation on [fragments](https://reactjs.org/docs/fragments.html) for more details.
- **Portals**. Let you render children into a different DOM subtree. See the documentation on [portals](https://reactjs.org/docs/portals.html) for more details.
- **String and numbers.** These are rendered as text nodes in the DOM.
- **Booleans or null**. Render nothing. (Mostly exists to support return test && <Child /> pattern, where test is boolean.)

The render() function should be pure, meaning that it does not modify component state, it returns the same result each time it’s invoked, and it does not directly interact with the browser.

If you need to interact with the browser, perform your work in componentDidMount() or the other lifecycle methods instead. Keeping render() pure makes components easier to think about.

**Constructor() :**

**If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your React component.**

The constructor for a React component is called before it is mounted. When implementing the constructor for a React.Component subclass, you should call super(props) before any other statement. Otherwise, this.props will be undefined in the constructor, which can lead to bugs.

Typically, in React constructors are only used for two purposes:

- Initializing [local state](https://reactjs.org/docs/state-and-lifecycle.html) by assigning an object to this.state.
- Binding [event handler](https://reactjs.org/docs/handling-events.html) methods to an instance.

You **should not call setState()** in the constructor(). Instead, if your component needs to use local state, **assign the initial state to this.state** directly in the constructor:


**Note**

Avoid copying props into state! This is a common mistake:

The problem is that it’s both unnecessary (you can use this.props.color directly instead),

**ComponentDidMount() :**

componentDidMount() is invoked immediately after a component is mounted (inserted into the tree). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.

This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in componentWillUnmount().

You **may call setState() immediately** in componentDidMount(). It will trigger an extra rendering, but it will happen before the browser updates the screen. This guarantees that even though the render() will be called twice in this case, the user won’t see the intermediate state. Use this pattern with caution because it often causes performance issues. In most cases, you should be able to assign the initial state in the constructor() instead. It can, however, be necessary for cases like modals and tooltips when you need to measure a DOM node before rendering something that depends on its size or position.

**ComponentDidUpdate() :**

componentDidUpdate() is invoked immediately after updating occurs. This method is not called for the initial render.

Use this as an opportunity to operate on the DOM when the component has been updated. This is also a good place to do network requests as long as you compare the current props to previous props (e.g. a network request may not be necessary if the props have not changed). 


componentDidUpdate(prevProps) {

`  `// Typical usage (don't forget to compare props):

`  `if (this.props.userID !== prevProps.userID) {

`    `this.fetchData(this.props.userID);

`  `}

}

You **may call setState() immediately** in componentDidUpdate() but note that **it must be wrapped in a condition** like in the example above, or you’ll cause an infinite loop. It would also cause an extra re-rendering which, while not visible to the user, can affect the component performance. If you’re trying to “mirror” some state to a prop coming from above, consider using the prop directly instead. Read more about [why copying props into state causes bugs](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html).

**ComponentWillUnmount () :**

componentWillUnmount() is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in componentDidMount().

You **should not call setState()** in componentWillUnmount() because the component will never be re-rendered. Once a component instance is unmounted, it will never be mounted again.




