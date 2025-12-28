# Immutability in State

## 🎯 What is Immutability?
**Never modify existing state directly**. Always create a **new copy** with the changes.

---

## ❌ Why Mutation is Bad

```jsx
const [user, setUser] = useState({ name: 'John', age: 25 });

// ❌ WRONG - Mutating directly
user.name = 'Jane';  // This doesn't trigger re-render!
setUser(user);       // React thinks nothing changed

// ✅ CORRECT - Creating new object
setUser({ ...user, name: 'Jane' });  // New object, React re-renders
```

> [!warning] React compares references
> React checks if `oldState === newState`. If you mutate the same object, the reference stays the same, so React thinks nothing changed!

---

## 📦 Immutable Updates for Different Types

### Updating Objects

```jsx
const [person, setPerson] = useState({
  name: 'John',
  age: 25,
  address: { city: 'NYC', zip: '10001' }
});

// Update one field
setPerson({ ...person, name: 'Jane' });

// Update nested field
setPerson({
  ...person,
  address: { ...person.address, city: 'LA' }
});

// Update multiple fields
setPerson({ ...person, name: 'Jane', age: 26 });
```

### Updating Arrays

```jsx
const [items, setItems] = useState(['Apple', 'Banana']);

// ❌ WRONG - These mutate the array
items.push('Cherry');      // Don't do this
items[0] = 'Apricot';      // Don't do this
items.splice(1, 1);        // Don't do this

// ✅ ADD item
setItems([...items, 'Cherry']);           // At end
setItems(['Cherry', ...items]);           // At start
setItems([...items.slice(0, 1), 'Cherry', ...items.slice(1)]); // At index

// ✅ REMOVE item
setItems(items.filter(item => item !== 'Banana'));  // By value
setItems(items.filter((_, index) => index !== 1)); // By index

// ✅ UPDATE item
setItems(items.map(item => 
  item === 'Banana' ? 'Blueberry' : item
));

// ✅ REPLACE item by index
setItems(items.map((item, index) => 
  index === 1 ? 'Blueberry' : item
));
```

### Array of Objects

```jsx
const [todos, setTodos] = useState([
  { id: 1, text: 'Learn React', done: false },
  { id: 2, text: 'Build app', done: false }
]);

// Toggle todo by id
setTodos(todos.map(todo =>
  todo.id === 1 
    ? { ...todo, done: !todo.done }  // New object for this todo
    : todo                            // Keep others unchanged
));

// Remove todo
setTodos(todos.filter(todo => todo.id !== 1));

// Add todo
setTodos([...todos, { id: 3, text: 'Deploy', done: false }]);
```

---

## 🔧 Immutable Methods Reference

| Action | Mutating (❌) | Immutable (✅) |
|--------|--------------|----------------|
| Add | `push()` | `[...arr, item]` |
| Remove | `pop()`, `splice()` | `filter()` |
| Replace | `arr[i] = x` | `map()` |
| Sort | `sort()` | `[...arr].sort()` |
| Reverse | `reverse()` | `[...arr].reverse()` |

---

## 💡 Practical Example

```jsx
function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState('');

  const addTodo = () => {
    if (!input.trim()) return;
    // Immutable add
    setTodos([...todos, {
      id: Date.now(),
      text: input,
      done: false
    }]);
    setInput('');
  };

  const toggleTodo = (id) => {
    // Immutable update
    setTodos(todos.map(todo =>
      todo.id === id ? { ...todo, done: !todo.done } : todo
    ));
  };

  const deleteTodo = (id) => {
    // Immutable remove
    setTodos(todos.filter(todo => todo.id !== id));
  };

  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={addTodo}>Add</button>
      
      {todos.map(todo => (
        <div key={todo.id}>
          <input 
            type="checkbox" 
            checked={todo.done}
            onChange={() => toggleTodo(todo.id)}
          />
          <span>{todo.text}</span>
          <button onClick={() => deleteTodo(todo.id)}>Delete</button>
        </div>
      ))}
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Never mutate state directly
- [ ] Use spread `...` to copy objects/arrays
- [ ] Use `map()` to update items, `filter()` to remove
- [ ] Copy arrays before `sort()` and `reverse()`
- [ ] Immutability ensures React detects changes

[[index|← Back to Module]]
