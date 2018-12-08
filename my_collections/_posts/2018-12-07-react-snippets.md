---
layout: post
title: 'React Snippets'
categories: react snippets cheatsheets
id: 1
---

`React` is a JavaScript library primarly for building user interfaces.

### Components

---

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

class Hello extends React.Component {
  render() {
    return <div className="message-box">Hello {this.props.name}</div>;
  }
}

const el = document.body;
ReactDOM.render(<Hello name="Trey" />, el);
```

### Import multiple exports

---

```javascript
import React, {Component} from 'react'
import ReactDOM from 'react-dom'

class Hello extends Component {
  ...
}
```

### Properties

---

```javascript
<Video fullscreen={true} autoplay={false} />

render () {
  this.props.fullscreen
  const { fullscreen, autoplay } = this.props
  ...
}
```

_Note_: Use `this.props` to access properties passed to the component.

### States

---

```javascript
constructor(props) {
  super(props)
  this.state = { username: undefined }
}

this.setState({ username: 'TexasBullet26' })

render () {
  this.state.username
  const { username } = this.state
  ...
}
```

_Note_: Use states `{this.state}` to manage dynamic data. With Babel you can use `proposal-class-fields` and get rid of constructor:

```javascript
class Hello extends Component {
  state = { username: undefined };
  ...
}
```

### Nesting

---

```javascript
class Info extends Component {
  render() {
    const { avatar, username } = this.props;

    return (
      <div>
        <UserAvatar src={avatar} />
        <UserProfile username={username} />
      </div>
    );
  }
}
```

As of React v16.2.0, `fragments` can be used to return multiple children without adding extra wrapping nodes to the DOM:

```javascript
import React, { Component, Fragment } from 'react';

class Info extends Component {
  render() {
    const { avatar, username } = this.props;

    return (
      <Fragment>
        <UserAvatar src={avatar} />
        <UserProfile username={username} />
      </Fragment>
    );
  }
}
```

Nest components to separate concerns. See: [Composing Components]()

### Children

---

```javascript
<AlertBox>
  <h1>You have pending notifications</h1>
</AlertBox>;

class AlertBox extends Component {
  render() {
    return <div className="alert-box">{this.props.children}</div>;
  }
}
```

Children are passed as the children property.

## Defaults

### Setting default props

---

```javascript
Hello.defaultProps = {
  color: 'blue',
};
```

See: [defaultProps]()

### Setting default state

---

```javascript
class Hello extends Component {
  constructor(props) {
    super(props);
    this.state = { visible: true };
  }
}
```

See the default state in the `constructor()`.

And without constructor using `Babel` with `proposal-class-fields`:

```javascript
class Hello extends Component {
  state = { visible: true };
}
```

See: [Setting the default state]()

## Other components

### Functional components

---

```javascript
function MyComponent({ name }) {
  return <div className="message-box">Hello {name}</div>;
}
```

Functional components have no state. Also, their props are passed as the first parameter to a function.

See: [Function and Class Components]()

### Pure Components

---

```javascript
import React, {PureComponent} from 'react'

class MessageBox extends PureComponent {
  ...
}
```

Performance-optimized version of React.Component. Doesn't rerender if props/state hasn't changed.

See: [Pure components]()

### Component API

---

```javascript
this.forceUpdate()

this.setState({ ... })
this.setState(state => { ... })

this.state
this.props
```

These methods and properties are available for Component instances.

See: [Component API]()

## Lifecycle

### Mounting

---

`constructor(props)` - Before rendering
`componentWillMount()` - Don't use this
`render()` - Render
`componentDidMount()` - After rendering (DOM available)
`componentWillUnmount()` - Before DOM removal
`componentDidCatch()` - Catch errors (16+)

Set initial the state on `constructor()`. Add DOM `event handlers`, `timers` (etc) on `componentDidMount(), then remove them on`componentWillUnmount()`.

### Updating

---

`` -

## DOM nodes

### References

---

```javascript
class MyComponent extends Component {
  render() {
    return (
      <div>
        <input ref={el => (this.input = el)} />
      </div>
    );
  }

  componentDidMount() {
    this.input.focus();
  }
}
```

Allows access to DOM nodes.

See: [Refs and the DOM]()

### DOM Events

---

```javascript
class MyComponent extends Component {
  render() {
    <input
      type="text"
      value={this.state.value}
      onChange={event => this.onChange(event)}
    />;
  }

  onChange(event) {
    this.setState({ value: event.target.value });
  }
}
```

Pass functions to attributes like `onChange`.

See: [Events]()

## Other features

### Transferring props

---

```javascript
<VideoPlayer src="video.mp4" />;

class VideoPlayer extends Component {
  render() {
    return <VideoEmbed {...this.props} />;
  }
}
```

Propagates `src="..."` down to the sub-component.

See: [Transferring props]()

### Top-level API

```javascript
```
