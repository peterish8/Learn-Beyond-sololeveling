# The Key Prop

## 🎯 What is the Key Prop?
A special attribute that helps React identify which items changed, added, or removed in a list.

```jsx
<li key={item.id}>{item.name}</li>
```

---

## ❓ Why Keys Matter

Without keys, React re-renders the entire list inefficiently. With keys, React knows exactly what changed.

| Without Keys | With Keys |
|--------------|-----------|
| Re-renders everything | Only updates changed items |
| Slow for large lists | Fast and efficient |
| May lose component state | Preserves component state |
| React warns in console | No warnings |

---

## ✅ Good Keys

```jsx
// ✅ Unique ID from database
{users.map(user => (
  <UserCard key={user.id} user={user} />
))}

// ✅ Unique string
{emails.map(email => (
  <li key={email}>{email}</li>
))}

// ✅ Generated ID (if no natural key)
{items.map(item => (
  <Item key={item.uuid} item={item} />
))}
```

---

## ❌ Bad Keys

```jsx
// ❌ Random number - changes every render!
{items.map(item => (
  <li key={Math.random()}>{item}</li>
))}

// ❌ Index (often problematic - see next note)
{items.map((item, index) => (
  <li key={index}>{item}</li>
))}

// ❌ Non-unique value
{users.map(user => (
  <li key={user.role}>{user.name}</li>  // Multiple users can have same role!
))}

// ❌ No key at all
{items.map(item => (
  <li>{item}</li>  // React will warn!
))}
```

---

## 🔑 Key Requirements

1. **Unique** among siblings
2. **Stable** (doesn't change between renders)
3. **Not random** (same item = same key always)

```jsx
// ✅ Each key is unique and stable
const users = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' }
];

{users.map(user => (
  <div key={user.id}>{user.name}</div>
))}
```

---

## 🎯 What Keys Do

### Preserve Component State
```jsx
function TodoItem({ todo }) {
  const [isEditing, setIsEditing] = useState(false);
  
  return (
    <div>
      {isEditing ? (
        <input />
      ) : (
        <span>{todo.text}</span>
      )}
      <button onClick={() => setIsEditing(!isEditing)}>Edit</button>
    </div>
  );
}

// With correct keys, editing state is preserved when list reorders
{todos.map(todo => (
  <TodoItem key={todo.id} todo={todo} />
))}
```

---

## 📋 Practical Examples

### User List
```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name} - {user.email}
        </li>
      ))}
    </ul>
  );
}
```

### Dynamic Components
```jsx
function Dashboard({ widgets }) {
  return (
    <div className="dashboard">
      {widgets.map(widget => (
        <Widget 
          key={widget.id}
          type={widget.type}
          data={widget.data}
        />
      ))}
    </div>
  );
}
```

### Nested Lists
```jsx
function Categories({ categories }) {
  return (
    <div>
      {categories.map(category => (
        <div key={category.id}>
          <h2>{category.name}</h2>
          <ul>
            {category.items.map(item => (
              <li key={item.id}>{item.name}</li>
            ))}
          </ul>
        </div>
      ))}
    </div>
  );
}
```

---

## ⚠️ Keys are Not Props

```jsx
function ListItem({ key, name }) {
  // ❌ Can't access key as a prop!
  console.log(key);  // undefined
  
  return <li>{name}</li>;
}

// ✅ Pass id separately if you need it
function ListItem({ id, name }) {
  console.log(id);  // Works!
  return <li>{name}</li>;
}

{items.map(item => (
  <ListItem key={item.id} id={item.id} name={item.name} />
))}
```

---

## 🎓 Key Takeaways

- [ ] Keys help React identify items in lists
- [ ] Must be unique among siblings
- [ ] Must be stable (don't use `Math.random()`)
- [ ] Usually use database ID
- [ ] Keys are not accessible as props

[[index|← Back to Module]]
