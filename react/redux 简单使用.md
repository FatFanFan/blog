---
title: Redux 简单使用
date: 2020-04-17 14:14:22
tags: React Redux
---


# Redux

## Store

**Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store**

```javascript
let store = createStore(counter);
```

1. state `const state = store.getState()`

   Redux 规定， 一个 State 对应一个 View。只要 State 相同，View 就相同。
   你知道 State，就知道 View 是什么样，反之亦然。

2. dispatch

   store.dispatch() 接受一个 Action 对象，将它分发出去

3. subscribe

   Store 允许使用 store.subscribe 方法设置监听函数，一旦 State 发生变化，就自动执行这个函数。

   store.subscribe 方法返回一个函数，调用这个函数就可以解除监听。

## Actions

**描述发生了什么**

```
{
  type: "ADD";
}
```

## Reducers

**Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer。**

**Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State**

```javascript
function counter(state = 0, action) {
  switch (action.type) {
    case "ADD":
      return state + 1;
    case "MINUS":
      return state - 1;
    default:
      return state;
  }
}
```

## 工作流程

首先，用户发出 Action。

`store.dispatch(action);`

然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action。
Reducer 会返回新的 State 。

```javascript
let nextState = counter(previousState, action);
```

State 一旦有变化，Store 就会调用监听函数。

// 设置监听函数
结合 React 的 hooks 可以更新数据

```javascript
const [number, setNumber] = useState(store.getState());

store.subscribe(() => setNumber(store.getState()));
```

[加减示例](https://codesandbox.io/s/ts-redux-l2r9n?file=/src/App.tsx)
