---
title: State Management Tools
tags:
  - React
categories: programming
---

The most popular example of state management is Redux

### Alternatives for state management in React

- Zustand
- Flux

### Redux Tool Kit (RTK)

### Zustand

create a `store.ts` in wherever you want

```Typescript
import { create } from "zustand";

interface BearState {
  bears: number;
  increasePopulation: () => void;
  removeAllBears: () => void;
  updateBears: (newBears: number) => void;
}

export const useStore = create<BearState>()((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })), // if you need to access the state
  removeAllBears: () => set({ bears: 0 }), // if you only need to set value
  updateBears: (newBears: number) => set({ bears: newBears }), // if you have input
}));
```
