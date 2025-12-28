# 🔧 Common Patterns

## Module Progress
- [ ] [[Component Composition Pattern]] 🏗️ Building with composable pieces
- [ ] [[Children Prop]] 👶 Passing content between tags
- [ ] [[Lifting State Up]] ⬆️ Sharing state between siblings
- [ ] [[Prop Drilling and Solutions]] 🕳️ Avoiding deep prop passing
- [ ] [[Render Props Pattern]] 🎭 Sharing logic via render functions
- [ ] [[Component Organization Tips]] 📂 Structuring for scale

---

## 🎯 Learning Objectives
- Compose components effectively
- Use the children prop for flexible layouts
- Lift state to the correct level
- Recognize and avoid prop drilling
- Understand the render props pattern
- Organize components for maintainability

## 📌 Key Concepts
> **Composition over inheritance**: Build UIs by combining small, focused components.

> **children prop**: `<Card>{content}</Card>` → `props.children` in Card

> **Lifting state up**: When siblings need shared state, move it to their common parent.

> **Prop drilling solutions**:
> - Context API (React built-in)
> - State management libraries (Redux, Zustand)
> - Component composition (reduce nesting)

[[React JS Hub|← Back to Hub]]
