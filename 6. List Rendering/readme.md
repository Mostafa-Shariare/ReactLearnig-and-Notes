## 🧠 What is List Rendering in React?

List rendering means **using JavaScript’s `.map()` method inside JSX** to loop through an array and render a piece of UI (like a component or element) for each item.

---

### 🔁 Basic Syntax

```jsx
array.map((item, index) => {
  return <JSXElement key={index} />;
});
```

> 🔑 **`key`** is super important — we’ll get into that soon.

---

## ✅ Example 1: Render a List of Strings

```jsx
function FruitsList() {
  const fruits = ["🍎 Apple", "🍌 Banana", "🍇 Grapes", "🍊 Orange"];

  return (
    <ul>
      {fruits.map((fruit, index) => (
        <li key={index}>{fruit}</li>
      ))}
    </ul>
  );
}
```

> ✔️ `map()` creates a new `<li>` for each fruit.

---

## ✅ Example 2: Render a List of Objects

```jsx
function Users() {
  const users = [
    { id: 1, name: "Alice", age: 24 },
    { id: 2, name: "Bob", age: 27 },
    { id: 3, name: "Charlie", age: 22 }
  ];

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>
          <h3>{user.name}</h3>
          <p>Age: {user.age}</p>
        </div>
      ))}
    </div>
  );
}
```

> 🔑 Always use a **unique key** (like `user.id`) instead of `index` if available!

---

## ✅ Example 3: List of Components

Sometimes you want each list item to be its **own component**. Let’s do that.

```jsx
function UserCard({ name, age }) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>Age: {age}</p>
    </div>
  );
}

function UserList() {
  const users = [
    { id: 1, name: "Dora", age: 25 },
    { id: 2, name: "Diego", age: 26 },
  ];

  return (
    <div>
      {users.map(user => (
        <UserCard key={user.id} name={user.name} age={user.age} />
      ))}
    </div>
  );
}
```

---

## 🔑 Why is the `key` Prop Important?

* React uses the `key` prop to **track which items changed, added, or removed**.
* Without a unique key, React can mess up re-rendering logic.

### ⚠️ Don’t do this unless you're sure:

```jsx
{items.map((item, index) => (
  <li key={index}>{item}</li> // ❌ using index as key — not ideal if list can change
))}
```

### ✅ Do this instead:

```jsx
{items.map(item => (
  <li key={item.id}>{item.name}</li> // ✅ stable and unique key
))}
```

---

## 🧪 Example 4: Conditional List Rendering + Filtering

```jsx
function TaskList() {
  const tasks = [
    { id: 1, name: "Do laundry", done: false },
    { id: 2, name: "Study React", done: true },
    { id: 3, name: "Cook dinner", done: false }
  ];

  return (
    <ul>
      {tasks
        .filter(task => !task.done)
        .map(task => (
          <li key={task.id}>{task.name}</li>
        ))}
    </ul>
  );
}
```

> 🔥 Combine `.filter()` and `.map()` for powerful dynamic UIs.

---

## 🧑‍💻 Bonus: Styling Even/Odd List Items

```jsx
function StyledList() {
  const items = ["One", "Two", "Three", "Four"];

  return (
    <ul>
      {items.map((item, index) => (
        <li
          key={index}
          style={{ color: index % 2 === 0 ? "blue" : "green" }}
        >
          {item}
        </li>
      ))}
    </ul>
  );
}
```

---

## 💡 Summary Table

| Concept              | Usage                               |
| -------------------- | ----------------------------------- |
| `.map()`             | Loop over array in JSX              |
| `key` prop           | Helps React track items             |
| Conditional `.map()` | Combine with `.filter()` or ternary |
| Component per item   | Keeps code clean and scalable       |


