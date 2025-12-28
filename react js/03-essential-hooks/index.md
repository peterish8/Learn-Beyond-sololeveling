# 🪝 Essential Hooks

## Module Progress
- [ ] [[useState Hook]] 💾 Managing component state
- [ ] [[useEffect Hook]] ⚡ Side effects & lifecycle
- [ ] [[useEffect Cleanup Functions]] 🧹 Preventing memory leaks
- [ ] [[useEffect Dependency Array]] 📋 Controlling when effects run
- [ ] [[Common Hooks Patterns]] 🔁 Frequently used patterns
- [ ] [[Custom Hooks Introduction]] 🛠️ Building reusable logic

---

## 🎯 Learning Objectives
- Use `useState` to add state to functional components
- Understand the `useEffect` lifecycle
- Write cleanup functions for effects
- Master the dependency array
- Recognize common hooks patterns
- Create simple custom hooks

## 📌 Key Concepts
> **useState** returns `[value, setValue]`. Call `setValue` to trigger a re-render.

> **useEffect** runs after render. Use it for data fetching, subscriptions, DOM manipulation.

> The dependency array `[]` controls WHEN the effect runs:
> - `[]` = once on mount
> - `[dep]` = when dep changes
> - no array = every render

[[React JS Hub|← Back to Hub]]
