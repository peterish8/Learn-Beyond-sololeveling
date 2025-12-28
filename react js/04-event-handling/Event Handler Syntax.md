# Event Handler Syntax

## 🎯 Function Reference vs Function Call

### ❌ WRONG - Calling the Function
```jsx
function App() {
  const handleClick = () => {
    console.log('Clicked!');
  };

  // ❌ Calls immediately, passes undefined to onClick
  return <button onClick={handleClick()}>Click</button>;
}
```

### ✅ CORRECT - Passing the Reference
```jsx
function App() {
  const handleClick = () => {
    console.log('Clicked!');
  };

  // ✅ Passes the function itself
  return <button onClick={handleClick}>Click</button>;
}
```

---

## 📝 Three Ways to Define Handlers

### 1. Separate Function (Best for Complex Logic)
```jsx
function App() {
  const handleClick = () => {
    console.log('Clicked!');
  };

  return <button onClick={handleClick}>Click</button>;
}
```

### 2. Inline Arrow Function (Best for Simple Logic)
```jsx
function App() {
  return (
    <button onClick={() => console.log('Clicked!')}>
      Click
    </button>
  );
}
```

### 3. Inline Function Expression (Rarely Used)
```jsx
function App() {
  return (
    <button onClick={function() { console.log('Clicked!') }}>
      Click
    </button>
  );
}
```

---

## ⚠️ Common Mistakes

### Mistake 1: Calling Instead of Passing
```jsx
// ❌ WRONG
<button onClick={handleClick()}>

// ✅ CORRECT
<button onClick={handleClick}>
```

### Mistake 2: Forgetting Arrow Function for Args
```jsx
const handleClick = (id) => {
  console.log('Clicked:', id);
};

// ❌ WRONG - Calls immediately
<button onClick={handleClick(123)}>

// ✅ CORRECT - Wraps in arrow function
<button onClick={() => handleClick(123)}>
```

### Mistake 3: Using Wrong Event Names
```jsx
// ❌ WRONG - lowercase
<button onclick={handleClick}>

// ✅ CORRECT - camelCase
<button onClick={handleClick}>
```

---

## 💡 When to Use Each Syntax

| Situation | Use |
|-----------|-----|
| Simple, one-line action | Inline arrow function |
| Need to pass arguments | Inline arrow function |
| Complex logic (5+ lines) | Separate function |
| Reused in multiple places | Separate function |
| Just calling a setter | Either works fine |

---

## 📋 Practical Examples

### Simple Setter
```jsx
const [count, setCount] = useState(0);

// Both are fine
<button onClick={() => setCount(count + 1)}>+</button>
<button onClick={() => setCount(prev => prev + 1)}>+</button>
```

### With Arguments
```jsx
const deleteItem = (id) => {
  console.log('Deleting:', id);
};

// Must wrap in arrow function
<button onClick={() => deleteItem(123)}>Delete</button>
```

### Complex Handler
```jsx
function App() {
  const handleSubmit = async () => {
    try {
      const response = await fetch('/api/submit');
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  };

  // Separate function for complex logic
  return <button onClick={handleSubmit}>Submit</button>;
}
```

---

## 🎓 Key Takeaways

- [ ] Pass function reference: `onClick={func}` ✅
- [ ] Don't call: `onClick={func()}` ❌
- [ ] Use arrow function to pass args: `onClick={() => func(arg)}`
- [ ] Use camelCase: `onClick`, `onChange`, etc.
- [ ] Separate complex handlers, inline simple ones

[[index|← Back to Module]]
