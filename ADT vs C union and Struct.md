please explain differences between algebraic data type and c union and struct

### Differences Between Algebraic Data Types, C Unions, and C Structs

**1. Algebraic Data Types (ADTs):**
Algebraic Data Types are a feature of functional programming languages like Haskell, ML, and Scala. They come in two main forms:

- **Sum Types**: Allow for multiple possible types (similar to C unions but safer). E.g., in Haskell:
  ```haskell
  data Shape = Circle Float | Rectangle Float Float
  ```
  Here, `Shape` can either be a `Circle` or a `Rectangle`, but not both simultaneously.

- **Product Types**: Combine multiple values into a single composite value (similar to C structs). E.g., in Haskell:
  ```haskell
  data Point = Point Float Float
  ```
  Here, `Point` combines two `Float` values.

Key characteristics:
- **Type Safety**: ADTs ensure safety by enforcing that only valid constructors and fields are accessible.
- **Pattern Matching**: Often used with ADTs to work with different types in a concise and expressive way.
- **Immutability**: Data is typically immutable.
- **High-level Abstraction**: ADTs are designed for high-level programming and often integrate with the type system to provide compile-time guarantees.

---

**2. C Union:**
A `union` in C is a memory-efficient data structure where all members share the same memory space, meaning only one member can be used at a time.

Example:
```c
union Data {
    int i;
    float f;
    char str[20];
};
```

Key characteristics:
- **Memory Efficiency**: All members occupy the same memory location.
- **Manual Type Management**: The programmer must keep track of which member is active; the compiler does not enforce type safety.
- **Low-Level Representation**: Ideal for cases where memory constraints are tight.
- **Unsafe by Default**: Accessing an inactive member leads to undefined behavior.

---

**3. C Struct:**
A `struct` in C is a composite data type that groups multiple variables together, where each member occupies its own memory.

Example:
```c
struct Point {
    float x;
    float y;
};
```

Key characteristics:
- **All Members Active**: All members exist simultaneously and occupy separate memory.
- **Type Safety at Field Level**: You can access specific fields safely, but C doesn’t ensure immutability or more advanced type-level guarantees.
- **Fixed Layout**: Fields are laid out in memory sequentially (with padding for alignment).
- **Efficient and Straightforward**: Useful for grouping related data.

---

### Key Differences Summary

| **Feature**             | **Algebraic Data Types**                     | **C Union**                      | **C Struct**                      |
|--------------------------|---------------------------------------------|-----------------------------------|------------------------------------|
| **Memory Usage**         | Depends on constructor; efficient per case | Single memory location for all   | Separate memory for all fields    |
| **Type Safety**          | Enforced by compiler                       | Manual management; unsafe        | Partial (unsafe operations possible) |
| **Simultaneous Members** | Only one (Sum Type) or all (Product Type)  | Only one                         | All                               |
| **Compile-Time Checks**  | Strong; prevents misuse                    | Weak                             | Limited                           |
| **Pattern Matching**     | Supported in functional languages          | Not applicable                   | Not applicable                    |
| **Intended Use**         | High-level modeling and abstraction        | Low-level memory optimization    | Grouping related fields           |

In essence, ADTs offer safer and more expressive ways to define data structures compared to C unions and structs, which are more manual and low-level in nature.
