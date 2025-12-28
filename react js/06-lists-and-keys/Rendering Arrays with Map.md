# Rendering Arrays with Map

## 🎯 The map() Method
Transforms an array into an array of JSX elements.

```jsx
const numbers = [1, 2, 3];
const listItems = numbers.map(num => <li>{num}</li>);

<ul>{listItems}</ul>
```

---

## 📝 Basic Example

```jsx
function FruitList() {
  const fruits = ['Apple', 'Banana', 'Cherry'];
  
  return (
    <ul>
      {fruits.map(fruit => (
        <li key={fruit}>{fruit}</li>
      ))}
    </ul>
  );
}
```

---

## 🔑 The key Prop (REQUIRED)

```jsx
// ✅ CORRECT - unique key
{users.map(user => (
  <UserCard key={user.id} user={user} />
))}

// ❌ WRONG - no key (React warning!)
{users.map(user => (
  <UserCard user={user} />
))}
```

---

## 💡 Common Patterns

### Objects Array
```jsx
function UserList() {
  const users = [
    { id: 1, name: 'John', age: 25 },
    { id: 2, name: 'Jane', age: 30 },
    { id: 3, name: 'Bob', age: 35 }
  ];
  
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name} - {user.age} years old
        </li>
      ))}
    </ul>
  );
}
```

### Component Rendering
```jsx
function ProductGrid({ products }) {
  return (
    <div className="grid">
      {products.map(product => (
        <ProductCard 
          key={product.id}
          name={product.name}
          price={product.price}
          image={product.image}
        />
      ))}
    </div>
  );
}
```

### With Index
```jsx
function ItemList() {
  const items = ['First', 'Second', 'Third'];
  
  return (
    <ol>
      {items.map((item, index) => (
        <li key={index}>
          {index + 1}. {item}
        </li>
      ))}
    </ol>
  );
}
```

---

## 📦 Inline vs Separate

### Inline (Simple Cases)
```jsx
<ul>
  {fruits.map(fruit => <li key={fruit}>{fruit}</li>)}
</ul>
```

### Separate (Complex Cases)
```jsx
const listItems = fruits.map(fruit => (
  <li key={fruit}>
    <span>{fruit}</span>
    <button>Delete</button>
  </li>
));

return <ul>{listItems}</ul>;
```

---

## 🎯 Practical Examples

### Todo List
```jsx
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li 
          key={todo.id}
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

### Table Rows
```jsx
function DataTable({ data }) {
  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Role</th>
        </tr>
      </thead>
      <tbody>
        {data.map(user => (
          <tr key={user.id}>
            <td>{user.name}</td>
            <td>{user.email}</td>
            <td>{user.role}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

### Cards Grid
```jsx
function CardGrid({ items }) {
  return (
    <div className="grid">
      {items.map(item => (
        <div key={item.id} className="card">
          <h3>{item.title}</h3>
          <p>{item.description}</p>
          <button>View</button>
        </div>
      ))}
    </div>
  );
}
```

---

## ⚠️ Empty Array Handling

```jsx
function UserList({ users }) {
  if (users.length === 0) {
    return <p>No users found</p>;
  }
  
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

// Or inline
function UserList({ users }) {
  return (
    <div>
      {users.length === 0 ? (
        <p>No users found</p>
      ) : (
        <ul>
          {users.map(user => <li key={user.id}>{user.name}</li>)}
        </ul>
      )}
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Use `.map()` to render arrays
- [ ] Always include unique `key` prop
- [ ] Key should be stable (usually `id`)
- [ ] Can map to any JSX element
- [ ] Handle empty arrays gracefully

[[index|← Back to Module]]
