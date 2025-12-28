# When to Use State vs Props

## 🎯 Quick Decision Guide

| Question | Answer |
|----------|--------|
| Does it come from a parent? | **Props** |
| Does it change over time? | **State** |
| Can it be computed from other data? | **Neither** (derive it) |
| Does it remain unchanged? | **Neither** (use const) |

---

## 📦 Props vs State Comparison

| Aspect | Props | State |
|--------|-------|-------|
| **Source** | Parent component | Component itself |
| **Mutable** | No (read-only) | Yes (via setter) |
| **Purpose** | Configure component | Track changes |
| **Updates** | Parent decides | Component decides |
| **Direction** | Top → Down | Local |

---

## 💡 Decision Flowchart

```
Does the data come from a parent?
├── YES → Use Props
└── NO ↓

Does it change over time in this component?
├── YES → Use State
└── NO ↓

Can it be calculated from props/state?
├── YES → Just compute it (no storage needed)
└── NO → Use a constant
```

---

## 📋 Examples

### ✅ Use Props When:

```jsx
// Data passed from parent
function UserCard({ name, email, avatar }) {
  return (
    <div>
      <img src={avatar} alt={name} />
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
}

// Configuration options
function Modal({ isOpen, title, onClose }) {
  if (!isOpen) return null;
  return (
    <div className="modal">
      <h2>{title}</h2>
      <button onClick={onClose}>Close</button>
    </div>
  );
}
```

### ✅ Use State When:

```jsx
// User input
function SearchBox() {
  const [query, setQuery] = useState('');
  return (
    <input 
      value={query} 
      onChange={(e) => setQuery(e.target.value)} 
    />
  );
}

// Toggle/switch
function Accordion() {
  const [isOpen, setIsOpen] = useState(false);
  return (
    <div>
      <button onClick={() => setIsOpen(!isOpen)}>Toggle</button>
      {isOpen && <p>Content here</p>}
    </div>
  );
}

// Fetched data
function UserList() {
  const [users, setUsers] = useState([]);
  
  useEffect(() => {
    fetch('/api/users')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);
  
  return <ul>{users.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

### ❌ Neither Needed:

```jsx
// Computed value - just calculate it
function CartTotal({ items }) {
  // ❌ Don't store in state
  // const [total, setTotal] = useState(0);
  
  // ✅ Just calculate
  const total = items.reduce((sum, item) => sum + item.price, 0);
  
  return <p>Total: ${total}</p>;
}

// Static data - use const
function Footer() {
  const year = new Date().getFullYear();  // Constant
  return <footer>© {year} My Company</footer>;
}
```

---

## 🔄 Props + State Together

Often components use both:

```jsx
function EditableUser({ initialName, onSave }) {
  // Props: initialName, onSave (from parent)
  // State: name (local, editable copy)
  
  const [name, setName] = useState(initialName);
  
  return (
    <div>
      <input 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
      />
      <button onClick={() => onSave(name)}>Save</button>
    </div>
  );
}
```

---

## ⚠️ Common Mistakes

```jsx
// ❌ Storing props in state unnecessarily
function Bad({ value }) {
  const [localValue, setLocalValue] = useState(value);
  // This creates sync issues!
}

// ✅ Just use the prop directly
function Good({ value }) {
  return <p>{value}</p>;
}

// ❌ Storing computed values in state
function Bad({ items }) {
  const [count, setCount] = useState(items.length);
  // This gets out of sync!
}

// ✅ Compute it
function Good({ items }) {
  const count = items.length;  // Always accurate
  return <p>{count} items</p>;
}
```

---

## 🎓 Key Takeaways

- [ ] Props = data from parent (read-only)
- [ ] State = local, changeable data
- [ ] Don't duplicate props in state
- [ ] Don't store computed values in state
- [ ] Start with props, add state when needed

[[index|← Back to Module]]
