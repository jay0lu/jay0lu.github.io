---
layout: default
title: React note
comments: true
---

# React note

### Call `this.setState` from another function
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { weather: 'sunny' };
    this.makeSomeFog = this.makeSomeFog.bind(this);
  }

  makeSomeFog() {
    this.setState({
      weather: 'foggy'
    });
  }
}
```
Due to the way that event handlers are bound in JavaScript, `this.toggleMood()` loses its `this` when it is used on line 20. Therefore, the expressions `this.state.mood` and `this.setState` won't mean what they're supposed to... unless you have already bound the correct this to `this.toggleMood`.

That is why we must bind `this.toggleMood` to this.

Or use arrow function
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { weather: 'sunny' };
    this.makeSomeFog = this.makeSomeFog.bind(this);
  }

  makeSomeFog = () => {
    this.setState({
      weather: 'foggy'
    });
  }
}
```


### React re-render
Any time that you call this.setState(), this.setState() AUTOMATICALLY calls .render() as soon as the state has changed.


### Event handler
For example, in <form />, onClick will return an event. To handle the event, need to get the event's value. To get the value string, create a event handler `handleClick`. Because the handleClick uses this, so need the `constructor` to bind .this.
```
export class Menu extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick(e) {
    const text = e.target.value;
    this.props.chooseVideo(text);
  }

  render() {
    return (
      <form onClick={this.handleClick}>
        <input type="radio" name="src" value="fast" /> fast
        <input type="radio" name="src" value="slow" /> slow
        <input type="radio" name="src" value="cute" /> cute
        <input type="radio" name="src" value="eek" /> eek
      </form>
    );
  }
}
```

### React style
Style needs to be a string or number (assume unit is px)
```
const styles = {
  marginTop:       "20px",
  backgroundColor: "green",
  fontSize:         50
};
```

### Stateless Functional Components and Props
```
// Normal way to display a prop using a variable:
export class MyComponentClass extends React.component {
  render() {
  	let title = this.props.title;
    return <h1>{title}</h1>;
  }
}

// Stateless functional component way to display a prop using a variable:
export const MyComponentClass = (props) => {
	let title = props.title;
  return <h1>{title}</h1>;
}
```

### PropTypes
PropTypes are useful for validation and documentation.
```
Runner.propTypes = {
  message:   React.PropTypes.string.isRequired,
  style:     React.PropTypes.object.isRequired,
  isMetric:  React.PropTypes.bool.isRequired,
  miles:     React.PropTypes.number.isRequired,
  milesToKM: React.PropTypes.func.isRequired,
  races:     React.PropTypes.array.isRequired
};
```

### Controlled vs Uncontrolled
An uncontrolled component is a component that maintains its own internal state. A controlled component is a component that does not maintain any internal state. Since a controlled component has no state, it must be controlled by someone else.

The fact that `<input />` keeps track of information makes it an uncontrolled component. It maintains its own internal state, by remembering data about itself.

A controlled component, on the other hand, has no memory. If you ask it for information about itself, then it will have to get that information through props. Most React components are controlled.

In React, when you give an `<input />` a value attribute, then something strange happens: the `<input />` BECOMES controlled. It stops using its internal storage. This is a more 'React' way of doing things.

### Lifecycle
Lifecycle methods are methods that get called at certain moments in a component's life.

You can write a lifecycle method that gets called right before a component renders for the first time.
You can write a lifecycle method that gets called right after a component renders, every time except for the first time.
You can attach lifecycle methods to a lot of different moments in a component's life. This has powerful implications!

There are three categories of lifecycle methods: mounting, updating, and unmounting.
A component "mounts" when it renders for the first time. This is when mounting lifecycle methods get called.
There are three mounting lifecycle methods:
- componentWillMount
- render
- componentDidMount

When a component mounts, it automatically calls these three methods, in order.

### Updating Lifecycle Methods
The first time that a component instance renders, it does not update. A component updates every time that it renders, starting with the second render.
There are five updating lifecycle methods:
- componentWillReceiveProps
- shouldComponentUpdate
- componentWillUpdate
- render
- componentDidUpdate

Whenever a component instance updates, it automatically calls all five of these methods, in order.

### this.setState()
Summary:
- Update to a component state should be done using setState()
- You can pass an object or a function to setState()
- Pass a function when you can to update state multiple times
- Do not depend on this.state immediately after calling setState() and make use of the updater function instead.


```
this.state.a = 1
this.setState(a: 2)
console.log(this.state.a)  //Output 1
```
Because `this.state.a` does not get update until the component has been re-rendered. setState() should be treated asynchronously — in other words, do not always expect that the state has changed after calling setState().

The solution is to use an updater. An updater allows you access the current state and put it to use immediately to update other items. So the changeCount() function will look like this.
```
changeCount = () => {
  this.setState((prevState) => {
    return { count: prevState.count - 1}
  })
}
```

When use `this.setState()` React calls reconciliation. The reconciliation process is the way React updates the DOM, by making changes to the component based on the change in state. When the request to setState() is triggered, React creates a new tree containing the reactive elements in the component (along with the updated state). This tree is used to figure out how the Search component’s UI should change in response to the state change by comparing it with the elements of the previous tree. React knows which changes to implement and will only update the parts of the DOM where necessary. This is why React is fast.

- We have a search component that displays a search term
- That search term is currently empty
- The user submits a search term
- That term is captured and stored by setState as a value
- Reconciliation takes place and React notices the change in value
- React instructs the search component to update the value and the search term is merged in

***

What are the features of React
- Virtual DOM instead of real DOM
- Server-side rendering
- Uni-direction data flow or databinding