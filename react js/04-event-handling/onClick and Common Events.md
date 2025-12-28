# onClick and Common Events

## 🎯 Common React Events

| Event | When It Fires |
|-------|---------------|
| `onClick` | User clicks element |
| `onChange` | Input value changes |
| `onSubmit` | Form is submitted |
| `onFocus` | Element receives focus |
| `onBlur` | Element loses focus |
| `onKeyPress` | Key is pressed (deprecated) |
| `onKeyDown` | Key is pressed down |
| `onKeyUp` | Key is released |
| `onMouseEnter` | Mouse enters element |
| `onMouseLeave` | Mouse leaves element |

---

## 📝 onClick

```jsx
function Button() {
  const handleClick = () => {
    alert('Button clicked!');
  };

  return <button onClick={handleClick}>Click Me</button>;
}

// Or inline
function Button() {
  return (
    <button onClick={() => alert('Clicked!')}>
      Click Me
    </button>
  );
}
```

---

## 📥 onChange (Inputs)

```jsx
function Input() {
  const [value, setValue] = useState('');

  return (
    <input 
      value={value}
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```

---

## 📤 onSubmit (Forms)

```jsx
function LoginForm() {
  const [email, setEmail] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();  // Don't reload page!
    console.log('Submitted:', email);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button type="submit">Login</button>
    </form>
  );
}
```

---

## ⌨️ Keyboard Events

```jsx
function SearchBox() {
  const [query, setQuery] = useState('');

  const handleKeyDown = (e) => {
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

---

## 🖱️ Mouse Events

```jsx
function Hoverable() {
  const [isHovered, setIsHovered] = useState(false);

  return (
    <div 
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
      style={{ 
        backgroundColor: isHovered ? 'lightblue' : 'white' 
      }}
    >
      Hover me!
    </div>
  );
}
```

---

## 🎯 Focus/Blur Events

```jsx
function Input() {
  const [isFocused, setIsFocused] = useState(false);

  return (
    <input 
      onFocus={() => setIsFocused(true)}
      onBlur={() => setIsFocused(false)}
      style={{ 
        borderColor: isFocused ? 'blue' : 'gray' 
      }}
    />
  );
}
```

---

## 📋 Complete Example

```jsx
function InteractiveForm() {
  const [form, setForm] = useState({ name: '', email: '' });
  const [submitted, setSubmitted] = useState(false);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prev => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    setSubmitted(true);
    console.log('Form submitted:', form);
  };

  const handleReset = () => {
    setForm({ name: '', email: '' });
    setSubmitted(false);
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input 
          name="name"
          value={form.name}
          onChange={handleChange}
          placeholder="Name"
        />
        <input 
          name="email"
          type="email"
          value={form.email}
          onChange={handleChange}
          placeholder="Email"
        />
        <button type="submit">Submit</button>
        <button type="button" onClick={handleReset}>Reset</button>
      </form>
      
      {submitted && <p>Thank you, {form.name}!</p>}
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Use `onClick` for clicks
- [ ] Use `onChange` for inputs
- [ ] Use `onSubmit` for forms (with preventDefault!)
- [ ] Use `onKeyDown` for keyboard shortcuts
- [ ] All events are camelCase in React

[[index|← Back to Module]]
