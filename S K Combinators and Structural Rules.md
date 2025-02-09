please explore correspondences between "s k combinators" "contraction weakening structural rules"

S K Combinators and Structural Rules

There are some interesting correspondences between **S and K combinators** in combinatory logic and **structural rules** in proof theory, particularly contraction and weakening. Let's break this down.

### **1. Background on S and K Combinators**
In combinatory logic:
- **K**: \( K x y = x \) (discards \( y \))
- **S**: \( S x y z = (x z) (y z) \) (distributes \( z \))

These combinators form a basis for computation, eliminating the need for explicit variables in lambda calculus.

### **2. Structural Rules in Proof Theory**
In sequent calculus and natural deduction, structural rules modify how assumptions are used:
- **Weakening**: Allows introducing an unused assumption:  
  \[
  \frac{\Gamma \vdash A}{\Gamma, B \vdash A}
  \]
- **Contraction**: Allows merging duplicate assumptions:  
  \[
  \frac{\Gamma, A, A \vdash B}{\Gamma, A \vdash B}
  \]

### **3. Correspondences Between S/K Combinators and Structural Rules**
1. **K and Weakening**:  
   - The **K combinator** implements weakening because it discards one of its arguments:  
     \( K x y = x \)  
   - Similarly, in proof theory, weakening allows introducing an unused assumption.

2. **S and Contraction**:  
   - The **S combinator** implements a form of contraction because it duplicates an argument:  
     \( S x y z = (x z) (y z) \)  
   - Here, \( z \) is applied twice, resembling contraction in logic.

### **4. Implications and Deeper Links**
- **Linear Logic**: In linear logic, contraction and weakening are restricted. Combinatory logic without K corresponds to a fragment of linear logic where weakening is not allowed.
- **Curry-Howard Correspondence**: The connection between logic and computation suggests that combinators can be interpreted as logical rules in type theory.
- **Lambda Calculus Restrictions**: Some functional programming languages avoid unrestricted weakening (e.g., linear and affine type systems).

### **5. Summary**
- **K corresponds to Weakening** (ignoring an argument).
- **S corresponds to Contraction** (duplicating an argument).
- This highlights deep connections between combinatory logic, proof theory, and type systems.

Would you like me to explore any specific aspect further?
