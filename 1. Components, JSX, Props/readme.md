

## 🧩 1. COMPONENTS in React

### 🔹 What is a Component?

A **component** is just a **JavaScript function** that returns **JSX (React HTML)**. Components are the building blocks of a React app.

There are two main types:

* **Functional Components** (modern & preferred)
* **Class Components** (older, rarely used now)

---

### ✅ Functional Component (Modern Syntax)

```jsx
// File: src/components/Greeting.jsx
function Greeting() {
  return <h1>Hello, React Buddy! 👋</h1>;
}

export default Greeting;
```

---

### 🧠 How to Use This Component?

```jsx
// File: src/App.jsx
import Greeting from './components/Greeting';

function App() {
  return (
    <div>
      <Greeting />
    </div>
  );
}

export default App;
```

> ✅ **Custom components must start with a capital letter** (`Greeting`, not `greeting`).

---

## 🎁 2. PROPS in React

### 🔹 What are Props?

**Props** (short for **properties**) are used to pass **data** from a parent component to a child component — like arguments to a function.

---

### ✅ Example of Props

```jsx
// File: src/components/Greeting.jsx
function Greeting(props) {
  return <h1>Hello, {props.name}! 👋</h1>;
}

export default Greeting;
```

```jsx
// File: src/App.jsx
import Greeting from './components/Greeting';

function App() {
  return (
    <div>
      <Greeting name="Shuvo" />
      <Greeting name="Mira" />
    </div>
  );
}
```

#### 🧠 Output:

```
Hello, Shuvo! 👋
Hello, Mira! 👋
```

---

### ✅ Destructuring Props (Modern Way)

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}! 👋</h1>;
}
```

---

### ✅ Passing Multiple Props

```jsx
function ProfileCard({ name, age, hobby }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Hobby: {hobby}</p>
    </div>
  );
}

export default ProfileCard;
```

```jsx
<ProfileCard name="Shuvo" age={21} hobby="Coding" />
```

---

## ⚛️ 3. JSX (JavaScript XML)

### 🔹 What is JSX?

**JSX** is a syntax extension that lets you write **HTML-like code inside JavaScript**. React uses it to describe the UI.

> JSX is **not HTML**, but it looks very similar!

---

### ✅ JSX Example

```jsx
const element = <h1>Hello JSX!</h1>;
```

Behind the scenes, this becomes:

```js
const element = React.createElement('h1', null, 'Hello JSX!');
```

---

### ✅ Rules of JSX

#### 1. Return only **one parent element**

❌ Wrong:

```jsx
return <h1>Hello</h1><p>World</p>;
```

✅ Right:

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

---

#### 2. Use `className` instead of `class`

```jsx
<div className="container">Welcome</div>
```

---

#### 3. Self-closing tags must end with `/`

```jsx
<img src="logo.png" alt="Logo" />
<br />
```

---

#### 4. Expressions go inside `{}`

```jsx
const name = "Shuvo";
return <h1>Hello, {name}</h1>;
```

---

### 🧠 JSX with Inline Style

```jsx
const headingStyle = {
  color: 'blue',
  fontSize: '24px'
};

return <h1 style={headingStyle}>Styled Text</h1>;
```

---

## 🔁 Full Mini Project: Greeting Cards

```jsx
// src/components/GreetingCard.jsx
function GreetingCard({ name, message }) {
  return (
    <div style={{ border: '1px solid gray', padding: '1rem', margin: '1rem' }}>
      <h2>Hello, {name}!</h2>
      <p>{message}</p>
    </div>
  );
}

export default GreetingCard;
```

```jsx
// src/App.jsx
import GreetingCard from './components/GreetingCard';

function App() {
  return (
    <div>
      <GreetingCard name="Shuvo" message="Welcome to React!" />
      <GreetingCard name="Mira" message="You're awesome!" />
    </div>
  );
}

export default App;
```

---

## 📦 Recap

| Concept       | Description                |
| ------------- | -------------------------- |
| **Component** | Function that returns JSX  |
| **Props**     | Data passed to a component |
| **JSX**       | HTML-like syntax inside JS |




[Next⏭️](https://github.com/Mostafa-Shariare/ReactLearnig-and-Notes/blob/main/2.%20Hooks%20and%20State/readme.md)
