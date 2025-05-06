## 🔄 What is **Prop Drilling**?

**Prop Drilling** is a situation in React where you pass data from a parent component to a deeply nested child component **through all the intermediate components**, even if they don't need the data themselves.

---

### ✅ Example of Prop Drilling:

Let’s say we want to pass the `userName` from a top-level `App` component to a deeply nested `Profile` component.

```jsx
// App.js
import React from 'react';
import Dashboard from './Dashboard';

function App() {
  const userName = "Tanvir";
  return (
    <div>
      <h1>Welcome to App</h1>
      <Dashboard userName={userName} />
    </div>
  );
}

export default App;
```

```jsx
// Dashboard.js
import React from 'react';
import Sidebar from './Sidebar';

function Dashboard({ userName }) {
  return (
    <div>
      <h2>Dashboard</h2>
      <Sidebar userName={userName} />
    </div>
  );
}

export default Dashboard;
```

```jsx
// Sidebar.js
import React from 'react';
import Profile from './Profile';

function Sidebar({ userName }) {
  return (
    <div>
      <h3>Sidebar</h3>
      <Profile userName={userName} />
    </div>
  );
}

export default Sidebar;
```

```jsx
// Profile.js
import React from 'react';

function Profile({ userName }) {
  return <p>User Name: {userName}</p>;
}

export default Profile;
```

### 😩 Problem:

If you have **lots of levels**, passing props through every component becomes **tedious** and **hard to manage**.

---

## 💡 Solution: `useContext()` + Context API

Instead of passing data manually at every level, React provides the **Context API** that allows you to share data **globally** to all components — no matter how deeply nested.

---

### ✅ Step-by-Step: Using `useContext()` and `createContext`

---

### 1️⃣ Create Context

```jsx
// UserContext.js
import { createContext } from 'react';

const UserContext = createContext();

export default UserContext;
```

---

### 2️⃣ Provide the context at a higher level

```jsx
// App.js
import React from 'react';
import Dashboard from './Dashboard';
import UserContext from './UserContext';

function App() {
  const userName = "Tanvir";
  return (
    <UserContext.Provider value={userName}>
      <div>
        <h1>Welcome to App</h1>
        <Dashboard />
      </div>
    </UserContext.Provider>
  );
}

export default App;
```

---

### 3️⃣ Consume the context wherever needed (even deep down)

```jsx
// Profile.js
import React, { useContext } from 'react';
import UserContext from './UserContext';

function Profile() {
  const userName = useContext(UserContext);
  return <p>User Name: {userName}</p>;
}

export default Profile;
```

---

Now, you can **skip passing props** through `Dashboard` and `Sidebar`:

```jsx
// Dashboard.js
import React from 'react';
import Sidebar from './Sidebar';

function Dashboard() {
  return (
    <div>
      <h2>Dashboard</h2>
      <Sidebar />
    </div>
  );
}

export default Dashboard;
```

```jsx
// Sidebar.js
import React from 'react';
import Profile from './Profile';

function Sidebar() {
  return (
    <div>
      <h3>Sidebar</h3>
      <Profile />
    </div>
  );
}

export default Sidebar;
```

