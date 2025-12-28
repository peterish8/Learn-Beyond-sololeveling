# Using Index as Key

## 🎯 The Question
Can you use the array index as a key?

```jsx
{items.map((item, index) => (
  <li key={index}>{item}</li>
))}
```

**Answer:** Sometimes yes, but usually no.

---

## ✅ When Index is OK

### 1. Static List (Never Changes)
```jsx
const daysOfWeek = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

// ✅ OK - list never changes
{daysOfWeek.map((day, index) => (
  <li key={index}>{day}</li>
))}
```

### 2. No Reordering/Filtering
```jsx
// ✅ OK - just displaying, never modified
const credits = ['Director: John', 'Producer: Jane', 'Writer: Bob'];

{credits.map((credit, index) => (
  <p key={index}>{credit}</p>
))}
```

### 3. No Unique ID Available (Last Resort)
```jsx
// ✅ Acceptable if no other option and list is simple
{simpleStrings.map((str, index) => (
  <span key={index}>{str}</span>
))}
```

---

## ❌ When Index is BAD

### 1. Dynamic Lists (Add/Remove/Reorder)
```jsx
// ❌ WRONG - items can be added/removed
function TodoList({ todos, onRemove }) {
  return (
    <ul>
      {todos.map((todo, index) => (
        <li key={index}>
          {todo.text}
          <button onClick={() => onRemove(index)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}

// ✅ CORRECT - use unique ID
{todos.map(todo => (
  <li key={todo.id}>
    {todo.text}
    <button onClick={() => onRemove(todo.id)}>Delete</button>
  </li>
))}
```

### 2. Lists That Can be Sorted/Filtered
```jsx
// ❌ WRONG - index changes when sorted
{sortedUsers.map((user, index) => (
  <UserCard key={index} user={user} />
))}

// ✅ CORRECT - ID stays same even when sorted
{sortedUsers.map(user => (
  <UserCard key={user.id} user={user} />
))}
```

### 3. Items with State
```jsx
// ❌ WRONG - state gets confused when list changes
function EditableItem({ text }) {
  const [isEditing, setIsEditing] = useState(false);
  // State will break if items reorder!
}

{items.map((item, index) => (
  <EditableItem key={index} text={item.text} />
))}

// ✅ CORRECT
{items.map(item => (
  <EditableItem key={item.id} text={item.text} />
))}
```

---

## 🐛 The Problem with Index

### Example: Deleting Items

```jsx
// Initial list with index keys
0: key=0 → "Apple"
1: key=1 → "Banana"
2: key=2 → "Cherry"

// Delete "Banana" (index 1)
0: key=0 → "Apple"   ✅ Stays same
1: key=1 → "Cherry"  ❌ Key was 2, now 1! React thinks it's a different item!

// With ID keys instead
id=1: key=1 → "Apple"
id=2: key=2 → "Banana"
id=3: key=3 → "Cherry"

// Delete "Banana" (id=2)
id=1: key=1 → "Apple"   ✅ Still key=1
id=3: key=3 → "Cherry"  ✅ Still key=3
// React knows exactly what happened!
```

---

## 📋 Decision Tree

```
Does the list ever change (add/remove/reorder)?
├── YES → Use unique ID, NOT index
└── NO ↓

Do items have component state?
├── YES → Use unique ID, NOT index
└── NO ↓

Is there a unique identifier available?
├── YES → Use it
└── NO → Index is acceptable (but not ideal)
```

---

## 💡 Generating IDs

If you don't have IDs, generate them:

```jsx
// Option 1: Add ID when creating
const [todos, setTodos] = useState([]);

const addTodo = (text) => {
  setTodos([...todos, {
    id: Date.now(),  // Simple ID
    text: text
  }]);
};

// Option 2: Use UUID library
import { v4 as uuidv4 } from 'uuid';

const addTodo = (text) => {
  setTodos([...todos, {
    id: uuidv4(),
    text: text
  }]);
};
```

---

## 🎓 Key Takeaways

- [ ] Index as key = OK only for static lists
- [ ] Index as key = BAD for dynamic lists
- [ ] Use unique ID whenever possible
- [ ] Index breaks when list changes order
- [ ] Generate IDs if none exist

[[index|← Back to Module]]
