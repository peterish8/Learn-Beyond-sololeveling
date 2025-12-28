# Passing Arguments to Handlers

## 🎯 The Problem
Event handlers in JSX don't automatically pass custom arguments.

```jsx
// ❌ This calls immediately
<button onClick={deleteItem(123)}>Delete</button>
```

---

## ✅ Solution: Arrow Function Wrapper

```jsx
const deleteItem = (id) => {
  console.log('Deleting:', id);
};

// Wrap in arrow function
<button onClick={() => deleteItem(123)}>Delete</button>
```

---

## 📦 Patterns

### 1. Single Argument
```jsx
function TodoList({ todos }) {
  const deleteTodo = (id) => {
    console.log('Delete:', id);
  };

  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>
          {todo.text}
          <button onClick={() => deleteTodo(todo.id)}>
            Delete
          </button>
        </li>
      ))}
    </ul>
  );
}
```

### 2. Multiple Arguments
```jsx
const updateUser = (id, field, value) => {
  console.log(`Update user ${id}: ${field} = ${value}`);
};

<button onClick={() => updateUser(123, 'name', 'John')}>
  Update
</button>
```

### 3. Event Object + Arguments
```jsx
const handleClick = (id, event) => {
  console.log('ID:', id);
  console.log('Event:', event);
};

// Event is passed automatically as last argument
<button onClick={(e) => handleClick(123, e)}>
  Click
</button>
```

---

## 🔄 Event Object First or Last?

### Event Last (Recommended)
```jsx
const handleClick = (id, event) => {
  console.log(id, event);
};

<button onClick={(e) => handleClick(123, e)}>Click</button>
```

### Event First
```jsx
const handleClick = (event, id) => {
  console.log(id, event);
};

<button onClick={(e) => handleClick(e, 123)}>Click</button>
```

---

## 💡 Practical Examples

### Delete Button in List
```jsx
function UserList({ users, onDelete }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name}
          <button onClick={() => onDelete(user.id)}>
            Delete
          </button>
        </li>
      ))}
    </ul>
  );
}
```

### Edit with Multiple Args
```jsx
function ProductCard({ product, onUpdate }) {
  return (
    <div>
      <h2>{product.name}</h2>
      <button onClick={() => onUpdate(product.id, 'stock', product.stock + 1)}>
        Add Stock
      </button>
      <button onClick={() => onUpdate(product.id, 'price', product.price * 0.9)}>
        Discount 10%
      </button>
    </div>
  );
}
```

### Toggle with ID
```jsx
function TodoList({ todos, onToggle }) {
  return (
    <ul>
      {todos.map(todo => (
        <li 
          key={todo.id}
          onClick={() => onToggle(todo.id)}
          style={{ 
            textDecoration: todo.done ? 'line-through' : 'none' 
          }}
        >
          {todo.text}
        </li>
      ))}
    </ul>
  );
}
```

---

## ⚠️ Performance Note

```jsx
// ❌ Creates new function every render (minor concern)
{todos.map(todo => (
  <button onClick={() => deleteTodo(todo.id)}>Delete</button>
))}

// ✅ Better for huge lists (advanced)
{todos.map(todo => (
  <button onClick={handleDelete} data-id={todo.id}>Delete</button>
))}

const handleDelete = (e) => {
  const id = e.target.dataset.id;
  deleteTodo(id);
};
```

> For most apps, the arrow function approach is fine. Only optimize if you have performance issues.

---

## 🎓 Key Takeaways

- [ ] Wrap in arrow function: `onClick={() => func(arg)}`
- [ ] Can pass multiple arguments
- [ ] Include event if needed: `(e) => func(arg, e)`
- [ ] Works in array maps for dynamic lists

[[index|← Back to Module]]
