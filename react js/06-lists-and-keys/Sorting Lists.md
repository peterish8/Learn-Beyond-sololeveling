# Sorting Lists

## 🎯 The sort() Method
**Important:** `sort()` mutates the original array! Copy first for immutability.

```jsx
// ❌ WRONG - mutates original
const sorted = items.sort();

// ✅ CORRECT - copy first
const sorted = [...items].sort();
```

---

## 📝 Basic Sorting

### Ascending (A → Z)
```jsx
const names = ['Charlie', 'Alice', 'Bob'];
const sorted = [...names].sort();
// ['Alice', 'Bob', 'Charlie']
```

### Descending (Z → A)
```jsx
const sorted = [...names].sort().reverse();
// ['Charlie', 'Bob', 'Alice']
```

---

## 💡 Sorting Numbers

```jsx
// ❌ WRONG - treats as strings!
[10, 2, 5].sort()  // [10, 2, 5] (wrong!)

// ✅ CORRECT - compare function
[10, 2, 5].sort((a, b) => a - b)  // [2, 5, 10]
```

### Ascending
```jsx
const numbers = [10, 2, 5, 8];
const ascending = [...numbers].sort((a, b) => a - b);
// [2, 5, 8, 10]
```

### Descending
```jsx
const descending = [...numbers].sort((a, b) => b - a);
// [10, 8, 5, 2]
```

---

## 🔧 Sorting Objects

### By String Property
```jsx
const users = [
  { id: 1, name: 'Charlie' },
  { id: 2, name: 'Alice' },
  { id: 3, name: 'Bob' }
];

// A → Z
const sorted = [...users].sort((a, b) => 
  a.name.localeCompare(b.name)
);

// Z → A
const sorted = [...users].sort((a, b) => 
  b.name.localeCompare(a.name)
);
```

### By Number Property
```jsx
const products = [
  { id: 1, price: 100 },
  { id: 2, price: 50 },
  { id: 3, price: 75 }
];

// Lowest to highest
const sorted = [...products].sort((a, b) => a.price - b.price);

// Highest to lowest
const sorted = [...products].sort((a, b) => b.price - a.price);
```

---

## 📋 Complete Examples

### Sort Users
```jsx
function UserList() {
  const [users, setUsers] = useState([...]);
  const [sortBy, setSortBy] = useState('name');
  
  const sortedUsers = [...users].sort((a, b) => {
    if (sortBy === 'name') {
      return a.name.localeCompare(b.name);
    }
    if (sortBy === 'age') {
      return a.age - b.age;
    }
    return 0;
  });
  
  return (
    <div>
      <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
        <option value="name">Sort by Name</option>
        <option value="age">Sort by Age</option>
      </select>
      
      <ul>
        {sortedUsers.map(user => (
          <li key={user.id}>{user.name} - {user.age}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Sort with Direction
```jsx
function ProductList() {
  const [products, setProducts] = useState([...]);
  const [sortField, setSortField] = useState('price');
  const [sortDir, setSortDir] = useState('asc');
  
  const sorted = [...products].sort((a, b) => {
    const multiplier = sortDir === 'asc' ? 1 : -1;
    
    if (sortField === 'name') {
      return multiplier * a.name.localeCompare(b.name);
    }
    if (sortField === 'price') {
      return multiplier * (a.price - b.price);
    }
    return 0;
  });
  
  return (
    <div>
      <select value={sortField} onChange={(e) => setSortField(e.target.value)}>
        <option value="name">Name</option>
        <option value="price">Price</option>
      </select>
      
      <button onClick={() => setSortDir(sortDir === 'asc' ? 'desc' : 'asc')}>
        {sortDir === 'asc' ? '↑' : '↓'}
      </button>
      
      <div>
        {sorted.map(product => (
          <ProductCard key={product.id} product={product} />
        ))}
      </div>
    </div>
  );
}
```

---

## ⚠️ Common Mistakes

```jsx
// ❌ WRONG - mutates state
users.sort((a, b) => a.name.localeCompare(b.name));

// ✅ CORRECT - creates new array
const sorted = [...users].sort((a, b) => a.name.localeCompare(b.name));
```

---

## 🎓 Key Takeaways

- [ ] Always copy array before sorting: `[...arr].sort()`
- [ ] Use compare function for numbers: `(a, b) => a - b`
- [ ] Use `localeCompare()` for strings
- [ ] Remember: `sort()` mutates original!
- [ ] Combine with filter and map as needed

[[index|← Back to Module]]
