please list formally specified no gc programming languages

[No GC Languages List]

Here’s a list of formally specified programming languages that do not include garbage collection (GC) as part of their runtime model. These languages often rely on manual memory management or deterministic techniques like stack allocation or reference counting.

---

### **Systems Programming Languages Without GC**
1. **C**  
   - Memory management is manual (using `malloc`, `free`, etc.).
   - The language specification does not include garbage collection.
   
2. **C++**  
   - Manual memory management or the use of smart pointers (`std::shared_ptr`, `std::unique_ptr`).
   - No garbage collection by design.

3. **Rust**  
   - No garbage collection; relies on an ownership model with compile-time checks for memory safety.
   - The specification emphasizes deterministic memory management.

4. **Ada**  
   - Does not require garbage collection, although implementations may optionally include it.
   - Memory is typically managed manually or with programmer-defined allocation strategies.

5. **Zig**  
   - Manual memory management.
   - The language avoids runtime overhead like GC, favoring explicit control.

6. **Fortran** (Modern versions)  
   - No garbage collection in the specification.
   - Memory is either managed manually or allocated statically.

7. **Assembly Language**  
   - No runtime memory management.
   - All memory control is at the instruction level.

8. **Modula-2**  
   - No garbage collection; manual memory management is typical.

9. **Pascal** (ISO Standard)  
   - Classic Pascal does not include garbage collection.
   - Memory is either statically or manually managed.

---

### **Low-Level Languages Designed for Performance**
1. **D (with GC optional)**  
   - The language allows disabling garbage collection, enabling manual or custom memory management.

2. **Nim**  
   - Garbage collection can be turned off; manual or custom memory allocators are supported.

3. **Go (when using allocators)**  
   - While Go generally uses garbage collection, it is possible to bypass GC with external memory management techniques in specialized applications.

4. **Carbon** (by Google, experimental)  
   - Aimed at systems programming without mandating garbage collection.

---

### **Real-Time or Safety-Critical Languages**
1. **SPARK (based on Ada)**  
   - A subset of Ada with stricter rules for safety-critical applications.
   - Avoids features that require garbage collection.

2. **MISRA C**  
   - A subset of C tailored for safety-critical applications where GC is not acceptable.

3. **VHDL**  
   - Used for hardware description; no concept of garbage collection.

4. **Verilog/SystemVerilog**  
   - Hardware description languages; no runtime memory management.

---

### **Historical Context: Non-GC Languages**
1. **Algol**  
   - No garbage collection; relies on block-structured allocation.
   
2. **COBOL**  
   - Designed for business applications with no garbage collection.

3. **PL/I**  
   - Does not include garbage collection.

4. **Forth**  
   - No garbage collection, with a stack-based memory model.

---

These languages offer precise memory control, making them suitable for performance-critical and safety-critical applications where the unpredictability of garbage collection is unacceptable.
