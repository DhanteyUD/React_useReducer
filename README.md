# React useReducer
`useReducer()` is a method from the React Hooks API, similar to useState but gives you more control to manage the state. It takes a reducer function and initial state as arguments and returns the state and dispatch method: `const [state, dispatch] = React`.

- [x] The `useReducer` Hook is similar to the `useState` Hook.
- [x] It allows for custom state logic.
- [x] If you find yourself keeping track of multiple pieces of state that rely on complex logic, `useReducer` may be useful.

> In React, useReducer essentially accepts a reducer function that returns a single value: const [count, dispatch] = useReducer(reducer, initialState); 
> The reducer function itself accepts two parameters and returns one value. The first parameter is the current state, and the second is the action.

## Syntax

The useReducer Hook accepts two arguments.

```js
useReducer(<reducer>, <initialState>)
```
The `reducer` function contains your custom state logic and the `initialState` can be a simple value but generally will contain an object.

The `useReducer` Hook returns the current state and a dispatch method.

Here is an example of `useReducer` in a counter app:

```js
import { useReducer } from "react";
import ReactDOM from "react-dom/client";

const initialTodo = [
  {
    id: 1,
    title: "Todo 1",
    complete: false,
  },
  {
    id: 2,
    title: "Todo 2",
    complete: false,
  },
];

const reducer = (state, action) => {
  switch (action.type) {
    case "COMPLETE":
      return state.map((todo) => {
        if (todo.id === action.id) {
          return { ...todo, complete: !todo.complete };
        } else {
          return todo;
        }
      });
    default:
      return state;
  }
};

function Todo() {
  const [todos, dispatch] = useReducer(reducer, initialTodo);

  const handleComplete = (todo) => {
    dispatch({ type: "COMPLETE", id: todo.id });
  };

  return (
    <>
      {todos.map((todo) => (
        <div key={todo.id}>
          <label>
            <input
              type="checkbox"
              checked={todo.complete}
              onChange={() => handleComplete(todo)}
            />
            {todo.title}
          </label>
        </div>
      ))}
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Todo />);
```
This is just the logic to keep track of the todo complete status.

All of the logic to add, delete, and complete a todo could be contained within a single `useReducer` Hook by adding more actions.
