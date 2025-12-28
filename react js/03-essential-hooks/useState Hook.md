# useState Hook

## 🎯 What is useState?
The most fundamental React hook. It lets you add **state** to functional components.

```jsx
import { useState } from 'react';
```

---

## 📝 Basic Syntax

```jsx
const [state, setState] = useState(initialValue);
```

| Part | Description |
|------|-------------|
| `state` | Current value |
| `setState` | Function to update value |
| `initialValue` | Starting value (any type) |

---

## 📦 Examples by Data Type

### Number
```jsx
const [count, setCount] = useState(0);

setCount(10);          // Set to 10
setCount(count + 1);   // Increment
setCount(prev => prev + 1);  // Increment (safe for batching)
```

### String
```jsx
const [name, setName] = useState('');

setName('John');
setName(prev => prev + '!');  // Append
```

### Boolean
```jsx
const [isOpen, setIsOpen] = useState(false);

setIsOpen(true);
setIsOpen(!isOpen);        // Toggle
setIsOpen(prev => !prev);  // Toggle (safer)
```

### Array
```jsx
const [items, setItems] = useState([]);

setItems(['a', 'b', 'c']);          // Replace
setItems([...items, 'new']);        // Add
setItems(items.filter(i => i !== 'a'));  // Remove
```

### Object
```jsx
const [user, setUser] = useState({ name: '', age: 0 });

setUser({ name: 'John', age: 25 });        // Replace
setUser({ ...user, name: 'Jane' });        // Update field
setUser(prev => ({ ...prev, age: 26 }));   // Update with previous
```

---

## ⚡ Functional Updates

Use a function when new state depends on previous state:

```jsx
// ❌ May not work correctly with batching
setCount(count + 1);
setCount(count + 1);
// Result: count + 1 (not count + 2!)

// ✅ Works correctly
setCount(prev => prev + 1);
setCount(prev => prev + 1);
// Result: count + 2
```

---

## 🎯 Lazy Initial State

For expensive initial values, pass a function:

```jsx
// ❌ Runs every render (expensive!)
const [data, setData] = useState(expensiveCalculation());

// ✅ Runs only once
const [data, setData] = useState(() => expensiveCalculation());
```

---

## 📋 Multiple State Variables

```jsx
function Form() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [age, setAge] = useState(0);
  
  return (
    <form>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <input value={email} onChange={(e) => setEmail(e.target.value)} />
      <input value={age} onChange={(e) => setAge(Number(e.target.value))} />
    </form>
  );
}

// Or use single object state
function Form() {
  const [form, setForm] = useState({ name: '', email: '', age: 0 });
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prev => ({ ...prev, [name]: value }));
  };
  
  return (
    <form>
      <input name="name" value={form.name} onChange={handleChange} />
      <input name="email" value={form.email} onChange={handleChange} />
      <input name="age" value={form.age} onChange={handleChange} />
    </form>
  );
}
```

---

## 💡 Complete Example

```jsx
function TodoList() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState('');

  const addTodo = () => {
    if (!input.trim()) return;
    setTodos(prev => [...prev, {
      id: Date.now(),
      text: input,
      done: false
    }]);
    setInput('');
  };

  const toggleTodo = (id) => {
    setTodos(prev => prev.map(todo =>
      todo.id === id ? { ...todo, done: !todo.done } : todo
    ));
  };

  return (
    <div>
      <input 
        value={input} 
        onChange={(e) => setInput(e.target.value)}
        onKeyPress={(e) => e.key === 'Enter' && addTodo()}
      />
      <button onClick={addTodo}>Add</button>
      
      <ul>
        {todos.map(todo => (
          <li 
            key={todo.id}
            onClick={() => toggleTodo(todo.id)}
            style={{ textDecoration: todo.done ? 'line-through' : 'none' }}
          >
            {todo.text}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] `useState` adds state to functional components
- [ ] Returns `[value, setValue]` array
- [ ] Use spreads for objects/arrays (immutability)
- [ ] Use function form `prev => ...` for safe updates
- [ ] Use lazy init `() => value` for expensive computations

[[index|← Back to Module]]
