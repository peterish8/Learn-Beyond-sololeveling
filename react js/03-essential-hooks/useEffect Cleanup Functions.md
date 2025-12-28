# useEffect Cleanup Functions

## 🎯 What is Cleanup?
A function returned from `useEffect` that runs **before** the next effect or when the component unmounts. It's used to prevent memory leaks and bugs.

---

## 🧹 When to Use Cleanup

| Scenario | Need Cleanup? |
|----------|---------------|
| Event listeners | ✅ Yes |
| Timers (setTimeout, setInterval) | ✅ Yes |
| Subscriptions (WebSocket, etc.) | ✅ Yes |
| Fetch requests (with AbortController) | ✅ Yes |
| Direct DOM manipulation | ✅ Maybe |
| Simple data fetching | ❌ Usually no |
| Logging | ❌ No |

---

## 📝 Cleanup Syntax

```jsx
useEffect(() => {
  // Setup code here
  
  return () => {
    // Cleanup code here
  };
}, [dependencies]);
```

---

## 💡 Common Cleanup Patterns

### 1. Event Listeners
```jsx
function WindowSize() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => {
      setWidth(window.innerWidth);
    };

    // Setup: Add listener
    window.addEventListener('resize', handleResize);

    // Cleanup: Remove listener
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return <p>Width: {width}px</p>;
}
```

### 2. setInterval Timer
```jsx
function Clock() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    // Setup: Start interval
    const interval = setInterval(() => {
      setTime(new Date());
    }, 1000);

    // Cleanup: Stop interval
    return () => clearInterval(interval);
  }, []);

  return <p>{time.toLocaleTimeString()}</p>;
}
```

### 3. setTimeout
```jsx
function DelayedMessage() {
  const [visible, setVisible] = useState(false);

  useEffect(() => {
    // Setup: Schedule showing message
    const timeout = setTimeout(() => {
      setVisible(true);
    }, 3000);

    // Cleanup: Cancel if component unmounts early
    return () => clearTimeout(timeout);
  }, []);

  return visible ? <p>Hello!</p> : <p>Wait...</p>;
}
```

### 4. Fetch with Abort
```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const controller = new AbortController();

    fetch(`/api/users/${userId}`, { signal: controller.signal })
      .then(res => res.json())
      .then(data => setUser(data))
      .catch(err => {
        if (err.name !== 'AbortError') {
          console.error(err);
        }
      });

    // Cleanup: Abort fetch if userId changes
    return () => controller.abort();
  }, [userId]);

  return user ? <h1>{user.name}</h1> : <p>Loading...</p>;
}
```

### 5. WebSocket Subscription
```jsx
function LiveChat({ roomId }) {
  const [messages, setMessages] = useState([]);

  useEffect(() => {
    // Setup: Connect to WebSocket
    const socket = new WebSocket(`ws://server.com/room/${roomId}`);
    
    socket.onmessage = (event) => {
      setMessages(prev => [...prev, event.data]);
    };

    // Cleanup: Close connection
    return () => {
      socket.close();
    };
  }, [roomId]);

  return (
    <ul>
      {messages.map((msg, i) => <li key={i}>{msg}</li>)}
    </ul>
  );
}
```

---

## ⏱️ When Does Cleanup Run?

```jsx
useEffect(() => {
  console.log('Effect runs');
  
  return () => {
    console.log('Cleanup runs');
  };
}, [count]);
```

**Timeline:**
1. Component mounts → Effect runs
2. `count` changes → **Cleanup runs first**, then effect runs
3. Component unmounts → Cleanup runs

---

## ⚠️ Common Mistakes

```jsx
// ❌ WRONG - Forgetting cleanup
useEffect(() => {
  setInterval(() => console.log('tick'), 1000);
}, []);
// This creates a new interval on every render = memory leak!

// ✅ CORRECT - With cleanup
useEffect(() => {
  const id = setInterval(() => console.log('tick'), 1000);
  return () => clearInterval(id);
}, []);

// ❌ WRONG - Cleanup doesn't match setup
useEffect(() => {
  window.addEventListener('scroll', handleScroll);
  return () => {
    window.removeEventListener('resize', handleScroll); // Wrong event!
  };
}, []);

// ✅ CORRECT - Cleanup matches setup
useEffect(() => {
  window.addEventListener('scroll', handleScroll);
  return () => {
    window.removeEventListener('scroll', handleScroll);
  };
}, []);
```

---

## 🎓 Key Takeaways

- [ ] Return a function from `useEffect` for cleanup
- [ ] Cleanup runs before next effect and on unmount
- [ ] Always cleanup: timers, listeners, subscriptions
- [ ] Cleanup prevents memory leaks
- [ ] Cleanup must reverse the setup

[[index|← Back to Module]]
