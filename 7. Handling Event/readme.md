## 🔥 What are Events in React?

In React, **events** are actions triggered by users, like:

* Clicking a button
* Typing into an input field
* Hovering over something
* Submitting a form, etc.

React uses **synthetic events**, which are wrappers around the browser's native events. This makes event handling consistent across all browsers.

---

## ✅ Basic Syntax of Handling Events in React

### 🟢 Functional Component with Event Handler

```jsx
import React from 'react';

function ClickButton() {
  function handleClick() {
    alert('Button was clicked!');
  }

  return (
    <button onClick={handleClick}>Click Me</button>
  );
}

export default ClickButton;
```

### Explanation:

* `onClick` is the React event.
* We pass a function `handleClick` to handle the event.
* We don’t use `()` after `handleClick` because we want to **pass the function**, not call it immediately.

---

## 🔁 Passing Arguments to Event Handlers

Sometimes you want to pass data to the function. You can do this using an **arrow function**.

```jsx
function GreetUser() {
  function greet(name) {
    alert(`Hello, ${name}!`);
  }

  return (
    <div>
      <button onClick={() => greet('Alice')}>Greet Alice</button>
      <button onClick={() => greet('Bob')}>Greet Bob</button>
    </div>
  );
}
```

---

## 🔄 Handling Form Events

Let’s create a form that captures user input using `onChange` and `onSubmit`.

```jsx
import React, { useState } from 'react';

function FormExample() {
  const [inputValue, setInputValue] = useState('');

  function handleChange(event) {
    setInputValue(event.target.value);
  }

  function handleSubmit(event) {
    event.preventDefault(); // prevent page reload
    alert(`Submitted: ${inputValue}`);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={inputValue} onChange={handleChange} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Key Concepts:

* `event.target.value` gets the value of the input.
* `event.preventDefault()` prevents the default behavior of the form submission (page reload).

---

## 🧠 Common React Events

| Event                           | Description                       |
| ------------------------------- | --------------------------------- |
| `onClick`                       | Fires when an element is clicked  |
| `onChange`                      | Triggers when input changes       |
| `onSubmit`                      | Triggers when a form is submitted |
| `onMouseEnter` / `onMouseLeave` | For hover interactions            |
| `onKeyDown` / `onKeyUp`         | Keyboard press events             |
| `onFocus` / `onBlur`            | Focus and blur of input fields    |

---

## 🎯 Example: Mouse and Keyboard Events

```jsx
function MouseAndKeyboardEvents() {
  function handleMouseEnter() {
    console.log('Mouse entered');
  }

  function handleKeyDown(event) {
    console.log(`Key pressed: ${event.key}`);
  }

  return (
    <div>
      <div 
        onMouseEnter={handleMouseEnter} 
        style={{ border: '1px solid black', padding: '10px', marginBottom: '10px' }}
      >
        Hover over me
      </div>

      <input type="text" onKeyDown={handleKeyDown} placeholder="Type something..." />
    </div>
  );
}
```

---

## 🧱 Using `this` in Class Components

Even though **functional components with hooks** are popular now, here’s how events work in **class components** for completeness:

```jsx
import React, { Component } from 'react';

class ClickButtonClass extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.handleClick = this.handleClick.bind(this); // binding required
  }

  handleClick() {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Clicked {this.state.count} times
      </button>
    );
  }
}
```

In class components, you must **bind the handler** or use an **arrow function** to retain the correct `this` context.

---

## 📦 Arrow Function as Class Method (No Need to Bind)

```jsx
class ArrowButton extends React.Component {
  state = { msg: "Hello" };

  handleClick = () => {
    this.setState({ msg: "Clicked!" });
  }

  render() {
    return (
      <button onClick={this.handleClick}>{this.state.msg}</button>
    );
  }
}
```

---

## ⚙️ Multiple Event Handling

```jsx
function MultiEventHandler() {
  function handleFocus() {
    console.log('Input focused');
  }

  function handleBlur() {
    console.log('Input blurred');
  }

  function handleKeyPress(event) {
    if (event.key === 'Enter') {
      alert('Enter key was pressed!');
    }
  }

  return (
    <input 
      onFocus={handleFocus}
      onBlur={handleBlur}
      onKeyPress={handleKeyPress}
      placeholder="Try typing and pressing Enter"
    />
  );
}
```



