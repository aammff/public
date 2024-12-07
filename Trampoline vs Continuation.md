please explain differences between trampoline continuation

The concepts of **trampoline** and **continuation** are related to control flow and handling of computations, especially in functional programming and compiler design. They both help manage how functions are executed, but they do so in different ways.

---

### **Trampoline**
A **trampoline** is a technique used to repeatedly invoke functions in a loop, instead of using the call stack for recursive calls. This allows deep recursion to be handled without causing a stack overflow, effectively making the recursion "stackless."

**How it works:**
- Functions return control to a central "trampoline" instead of calling each other directly.
- Instead of making recursive calls, the function returns a **thunk** (a wrapped computation or function to be executed later).
- The trampoline repeatedly executes these thunks in a loop.

**Key Features:**
1. Avoids stack overflow by using iteration rather than recursion.
2. Used for implementing tail-recursive functions.
3. Relies on returning a value or a function to a "trampoline loop" that decides the next step.

**Example (Pseudo-JavaScript):**
```javascript
function trampoline(func) {
    let result = func;
    while (typeof result === "function") {
        result = result();
    }
    return result;
}

function factorial(n, acc = 1) {
    return n === 0
        ? acc
        : () => factorial(n - 1, n * acc); // Return a thunk
}

console.log(trampoline(() => factorial(10000)));
```

---

### **Continuation**
A **continuation** is an abstraction of "what to do next" in a computation. It represents the rest of the program (or computation) at any given point. Continuations are commonly used in functional programming to manage control flow explicitly.

**How it works:**
- A function doesn't just return a value; it receives another function (the **continuation**) that it calls with the result.
- This allows functions to "pass the baton" of execution explicitly.

**Key Features:**
1. Provides explicit control over the execution flow.
2. Often used in **Continuation-Passing Style (CPS)**, where functions take an extra argument (the continuation).
3. Can be used to implement advanced control flow mechanisms like early exits, backtracking, coroutines, or exceptions.

**Example (Continuation-Passing Style in JavaScript):**
```javascript
function factorial(n, k) {
    return n === 0
        ? k(1) // Call the continuation with the result
        : factorial(n - 1, (result) => k(n * result));
}

// Start with the identity continuation
factorial(5, (result) => console.log(result)); // Outputs 120
```

---

### Key Differences

| **Aspect**              | **Trampoline**                                          | **Continuation**                                        |
|--------------------------|--------------------------------------------------------|--------------------------------------------------------|
| **Purpose**              | Avoid stack overflow by converting recursion to iteration. | Represent and manipulate "what to do next."            |
| **Mechanism**            | Uses a loop to execute thunks iteratively.              | Passes control explicitly through continuation functions. |
| **Stack Usage**          | Avoids using the call stack for recursive calls.         | Often uses the stack (unless tail-optimized).          |
| **Implementation Style** | Centralized control in a loop (trampoline loop).         | Decentralized via continuation-passing functions.      |
| **Use Cases**            | Tail recursion, asynchronous workflows.                 | CPS, advanced control flow (exceptions, coroutines).   |

---

In essence:
- Use **trampolines** to manage recursion in a stack-safe manner without altering the flow of the computation.
- Use **continuations** to explicitly control and transform the flow of computations, enabling sophisticated execution strategies.
