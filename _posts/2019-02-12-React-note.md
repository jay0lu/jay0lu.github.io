---
layout: default
title: Docker learning note
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


### React re-render
Any time that you call this.setState(), this.setState() AUTOMATICALLY calls .render() as soon as the state has changed.


### Event handler
For example, in <form />, onClick will return an event. To handle the event, need to get the event's value. To get the value string, create a event handler `handleClick`. Becaule the handleClick uses this, so need the `constructor` to bind .this.
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