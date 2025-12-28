# What is State

## 🎯 Definition
**State** is data that can **change over time** within a component. When state changes, React **re-renders** the component.

> Props = data from parent (read-only)
> State = data owned by component (can change)

---

## 🔄 State Makes Things Dynamic

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);  // State!
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

When you click the button:
1. `setCount` is called with new value
2. React updates the state
3. Component **re-renders** with new value
4. UI shows updated count

---

## 📦 useState Syntax

```jsx
const [value, setValue] = useState(initialValue);
```

| Part | Description |
|------|-------------|
| `value` | Current state value |
| `setValue` | Function to update state |
| `initialValue` | Starting value (any type) |

---

## 📋 State Examples

### String State
```jsx
const [name, setName] = useState('');

<input 
  value={name} 
  onChange={(e) => setName(e.target.value)} 
/>
```

### Boolean State
```jsx
const [isVisible, setIsVisible] = useState(false);

<button onClick={() => setIsVisible(!isVisible)}>
  Toggle
</button>
{isVisible && <Modal />}
```

### Number State
```jsx
const [count, setCount] = useState(0);

setCount(count + 1);  // Increment
setCount(count - 1);  // Decrement
setCount(0);          // Reset
```

### Array State
```jsx
const [items, setItems] = useState([]);

// Add item
setItems([...items, newItem]);

// Remove item
setItems(items.filter(item => item.id !== id));
```

### Object State
```jsx
const [user, setUser] = useState({ name: '', age: 0 });

// Update one property
setUser({ ...user, name: 'John' });
```

---

## ⚠️ State Rules

### 1. Never Modify State Directly
```jsx
// ❌ WRONG
count = count + 1;
items.push(newItem);
user.name = 'John';

// ✅ CORRECT
setCount(count + 1);
setItems([...items, newItem]);
setUser({ ...user, name: 'John' });
```

### 2. State Updates Are Asynchronous
```jsx
setCount(count + 1);
console.log(count);  // Still shows OLD value!

// Use callback for sequential updates
setCount(prev => prev + 1);
setCount(prev => prev + 1);  // This works!
```

### 3. State is Component-Local
```jsx
// Each instance has its own state
<Counter />  // Has its own count
<Counter />  // Has its own count (separate)
```

---

## 💡 When to Use State

| Situation | Use State? |
|-----------|------------|
| Form input values | ✅ Yes |
| Toggle visibility | ✅ Yes |
| Fetched data | ✅ Yes |
| Counter/timer | ✅ Yes |
| Current user | ✅ Yes |
| Static text | ❌ No (use const) |
| Derived data | ❌ No (compute it) |

---

## 🎓 Key Takeaways

- [ ] State = changeable data in a component
- [ ] `useState` returns `[value, setValue]`
- [ ] State changes trigger re-renders
- [ ] Never mutate state directly
- [ ] State updates are asynchronous

[[index|← Back to Module]]
