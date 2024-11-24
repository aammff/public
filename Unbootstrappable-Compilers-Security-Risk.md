please explain "unbootstrappable compilers considered unsafe"


The phrase "unbootstrappable compilers considered unsafe" likely refers to a discussion in computer science about the trustworthiness and security of compilers that cannot be verified through a process called **bootstrapping**.

### What is a Compiler?
A **compiler** is a program that translates code written in a high-level programming language (like C or Python) into machine code that computers can execute.

### What is Bootstrapping in the Context of Compilers?
Bootstrapping a compiler involves:
1. Writing a simple version of the compiler in a minimal language.
2. Using this simple compiler to build a more advanced version of itself.
3. Repeating this process to gradually build a robust compiler.

This process ensures that the compiler's correctness is traceable back to a trusted and verifiable starting point, often a minimal and simple toolchain.

### What Makes a Compiler "Unbootstrappable"?
A compiler is considered **unbootstrappable** if it cannot be used to compile itself, or if the process of building it from scratch is opaque, complex, or depends on unverified binaries. For example:
- The source code of the compiler may not exist.
- The compiler may depend on precompiled binaries that cannot be verified.
- It may involve circular dependencies, where the tools to build the compiler depend on the compiler itself.

### Why Are Unbootstrappable Compilers Considered Unsafe?
Unbootstrappable compilers are often seen as unsafe because:
1. **Trust Issues**: If you cannot trace and verify the origin of the compiler, you might inherit vulnerabilities, backdoors, or malicious code from unverified components. This was famously demonstrated by Ken Thompson in his "Reflections on Trusting Trust" talk, where he showed how a backdoor could persist in a compiler even if its source code appears clean.
   
2. **Lack of Transparency**: Without bootstrappability, there's no way to independently rebuild and audit the compiler, making it difficult to trust its outputs.

3. **Supply Chain Vulnerabilities**: If the compiler's binary is compromised (intentionally or unintentionally), every program it compiles, including future versions of itself, could also be compromised.

### Conclusion
Bootstrappable compilers are essential for maintaining trust in software development and security. They allow developers to trace a clear lineage from minimal, trusted tools to modern, complex compilers. Unbootstrappable compilers, in contrast, introduce uncertainty and potential vulnerabilities, which is why they are often deemed unsafe.
