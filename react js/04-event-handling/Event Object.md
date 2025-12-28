# Event Object

## 🎯 What is the Event Object?
An object that contains information about the event that occurred. Automatically passed to event handlers.

```jsx
const handleClick = (event) => {
  console.log(event);  // SyntheticBaseEvent { ... }
};

<button onClick={handleClick}>Click</button>
```

---

## 📦 Accessing the Event

### Automatically Available
```jsx
function App() {
  // Event is the first parameter
  const handleClick = (event) => {
    console.log('Clicked!', event);
  };

  return <button onClick={handleClick}>Click</button>;
}
```

### With Arrow Functions
```jsx
<button onClick={(event) => console.log(event)}>
  Click
</button>

// Or shorthand
<button onClick={(e) => console.log(e)}>
  Click
</button>
```

---

## 🔑 Common Event Properties

| Property | Description | Example Use |
|----------|-------------|-------------|
| `e.target` | Element that triggered event | `e.target.value` |
| `e.currentTarget` | Element handler is attached to | `e.currentTarget` |
| `e.type` | Event type | `'click'`, `'change'` |
| `e.key` | Key pressed (keyboard) | `'Enter'`, `'Escape'` |
| `e.preventDefault()` | Stop default behavior | Form submission |
| `e.stopPropagation()` | Stop event bubbling | Click bubbling |

---

## 💡 Practical Examples

### Getting Input Value
```jsx
function SearchBox() {
  const [query, setQuery] = useState('');

  const handleChange = (e) => {
    console.log(e.target.value);  // Current input value
    setQuery(e.target.value);
  };

  return <input value={query} onChange={handleChange} />;
}
```

### Getting Checkbox State
```jsx
function Checkbox() {
  const [checked, setChecked] = useState(false);

  const handleChange = (e) => {
    console.log(e.target.checked);  // true or false
    setChecked(e.target.checked);
  };

  return (
    <input 
      type="checkbox" 
      checked={checked} 
      onChange={handleChange} 
    />
  );
}
```

### Form with Multiple Inputs
```jsx
function Form() {
  const [form, setForm] = useState({ name: '', email: '' });

  const handleChange = (e) => {
    const { name, value } = e.target;  // Destructure from event.target
    setForm(prev => ({ ...prev, [name]: value }));
  };

  return (
    <form>
      <input name="name" value={form.name} onChange={handleChange} />
      <input name="email" value={form.email} onChange={handleChange} />
    </form>
  );
}
```

### Keyboard Events
```jsx
function SearchBox() {
  const [query, setQuery] = useState('');

  const handleKeyDown = (e) => {
    console.log('Key:', e.key);        // Which key
    console.log('Code:', e.code);      // Physical key
    console.log('Ctrl:', e.ctrlKey);   // Ctrl pressed?
    console.log('Shift:', e.shiftKey); // Shift pressed?

    if (e.key === 'Enter') {
      console.log('Search:', query);
    }
    if (e.key === 'Escape') {
      setQuery('');
    }
  };

  return (
    <input 
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      onKeyDown={handleKeyDown}
    />
  );
}
```

### Mouse Events
```jsx
function ImageViewer() {
  const handleClick = (e) => {
    console.log('X:', e.clientX);  // Mouse X position
    console.log('Y:', e.clientY);  // Mouse Y position
    console.log('Button:', e.button);  // 0 = left, 1 = middle, 2 = right
  };

  return (
    <img 
      src="photo.jpg" 
      onClick={handleClick}
      alt="Click me"
    />
  );
}
```

---

## 🆚 target vs currentTarget

```jsx
function Parent() {
  const handleClick = (e) => {
    console.log('target:', e.target);           // Element that was clicked
    console.log('currentTarget:', e.currentTarget);  // Element with handler
  };

  return (
    <div onClick={handleClick} style={{ padding: '20px', background: 'lightblue' }}>
      <button>Click me</button>
    </div>
  );
}

// If you click the button:
// target = <button>
// currentTarget = <div>
```

---

## 🎓 Key Takeaways

- [ ] Event object is auto-passed as first argument
- [ ] Use `e.target` to get element that triggered event
- [ ] Use `e.target.value` for input values
- [ ] Use `e.key` for keyboard events
- [ ] Use `e.preventDefault()` to stop default behavior

[[index|← Back to Module]]
