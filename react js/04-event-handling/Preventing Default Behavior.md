# Preventing Default Behavior

## 🎯 What is Default Behavior?
Browsers have built-in behaviors for certain events. Sometimes you want to **prevent** these.

| Element | Default Behavior |
|---------|------------------|
| `<a>` link | Navigate to URL |
| `<form>` submit | Reload page |
| Right-click | Show context menu |
| Checkbox | Toggle checked |

---

## 📝 Using preventDefault()

```jsx
event.preventDefault();
```

---

## 💡Common Use Cases

### 1. Prevent Form Submission
```jsx
function LoginForm() {
  const [email, setEmail] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();  // ← Don't reload page!
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

> [!warning] Always preventDefault on Forms
> Without it, the page will reload on submission!

---

### 2. Prevent Link Navigation
```jsx
function CustomLink() {
  const handleClick = (e) => {
    e.preventDefault();  // Don't navigate
    console.log('Link clicked, but not navigating');
  };

  return (
    <a href="https://google.com" onClick={handleClick}>
      Click me
    </a>
  );
}
```

---

### 3. Prevent Context Menu
```jsx
function NoRightClick() {
  const handleContextMenu = (e) => {
    e.preventDefault();  // Disable right-click menu
    console.log('Right-click disabled');
  };

  return (
    <div onContextMenu={handleContextMenu}>
      Right-click is disabled here
    </div>
  );
}
```

---

### 4. Prevent Drag/Drop Default
```jsx
function FileDropZone() {
  const handleDrop = (e) => {
    e.preventDefault();  // Don't open file in browser
    const files = e.dataTransfer.files;
    console.log('Files dropped:', files);
  };

  const handleDragOver = (e) => {
    e.preventDefault();  // Required for drop to work
  };

  return (
    <div 
      onDrop={handleDrop}
      onDragOver={handleDragOver}
      style={{ border: '2px dashed gray', padding: '20px' }}
    >
      Drop files here
    </div>
  );
}
```

---

## 🔄 preventDefault vs stopPropagation

```jsx
// preventDefault - stops browser's default action
e.preventDefault();

// stopPropagation - stops event from bubbling to parent
e.stopPropagation();

// Both can be used together
const handleClick = (e) => {
  e.preventDefault();
  e.stopPropagation();
};
```

---

## 📋 Complete Form Example

```jsx
function ContactForm() {
  const [form, setForm] = useState({
    name: '',
    email: '',
    message: ''
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prev => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();  // ← Crucial!

    // Validate
    if (!form.name || !form.email) {
      alert('Please fill all fields');
      return;
    }

    // Submit
    console.log('Submitting:', form);
    
    // Reset
    setForm({ name: '', email: '', message: '' });
  };

  return (
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
      <textarea 
        name="message"
        value={form.message}
        onChange={handleChange}
        placeholder="Message"
      />
      <button type="submit">Send</button>
    </form>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Use `e.preventDefault()` to stop browser defaults
- [ ] **Always** use on form `onSubmit`
- [ ] Use on links to prevent navigation
- [ ] Use on drag/drop to enable custom handling
- [ ] Different from `stopPropagation()` (bubbling)

[[index|← Back to Module]]
