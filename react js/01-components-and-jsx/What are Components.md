# What are Components

## 🎯 Overview
Components are the **building blocks** of any React application. Think of them like LEGO pieces – small, reusable parts that you combine to build something bigger.

---

## 📦 Two Types of Components

### 1. Functional Components (Modern Way ✅)
```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Arrow function version
const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

// With destructuring (cleanest)
const Greeting = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```

### 2. Class Components (Legacy Way)
```jsx
import React, { Component } from 'react';

class Greeting extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

---

## ⚡ Why Functional Components are Preferred

| Functional | Class |
|------------|-------|
| Less code | More boilerplate |
| Easier to read | Complex syntax |
| Use Hooks for state | Use `this.state` |
| Better performance | Slightly slower |
| Modern React standard | Legacy approach |

> [!tip] Always Use Functional
> As of React 16.8+, functional components with Hooks can do everything class components can. Use functional components for all new code!

---

## 🧩 Component Rules

1. **Name starts with Capital letter**: `MyComponent` not `myComponent`
2. **Must return JSX** (or null)
3. **One root element** per return (use Fragments if needed)
4. **Pure by default**: Same props → Same output

---

## 💡 Simple Example

```jsx
// Button.jsx
function Button({ text, onClick }) {
  return (
    <button onClick={onClick}>
      {text}
    </button>
  );
}

// Using the component
function App() {
  return (
    <div>
      <Button text="Click me" onClick={() => alert('Clicked!')} />
      <Button text="Submit" onClick={() => console.log('Submitted')} />
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Components are reusable UI pieces
- [ ] Use **functional components** (not class)
- [ ] Component names must be **Capitalized**
- [ ] Components receive data through **props**
- [ ] Components return **JSX**

[[index|← Back to Module]]
