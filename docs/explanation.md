Structure Explanation

---

**1. Lexical Analysis**
Handled by:

* `token/token.go`
* `lexer/lexer.go`

This is your scanner. Raw source code goes in, a stream of tokens comes out.
Keywords, identifiers, integers, operators, delimiters — all born here.

---

**2. Syntax Analysis**
Handled by:

* `parser/parser.go`
* `ast/ast.go`

The parser consumes tokens and produces an AST (Abstract Syntax Tree).
Your notes on Pratt parsing confirm this is a precedence-aware expression parser, which is exactly right.

---

**3. Semantic Analysis**
Handled by:

* `evaluator/evaluator.go`
* `object/object.go`
* `object/environment.go`

You don’t have a *separate* semantic analysis pass like a classical compiler. Instead, semantics are enforced during evaluation:

* Undefined variables → detected via `Environment`
* Type mismatches → detected during evaluation
* Invalid operations → runtime semantic errors

This is normal for interpreters.

---

**4. Code Optimization (Machine-independent)**
**Not present (explicitly).**

You do not have an optimization pass like:

* constant folding
* dead code elimination
* algebraic simplification

That said, some *implicit* optimization may occur if evaluation short-circuits expressions, but that’s incidental, not a designed phase.

---

**5. Storage Allocation**
Handled by:

* `object/environment.go`
* Go runtime (implicitly)

Variable bindings, scopes, lifetimes — all managed by `Environment`.
Memory allocation itself is delegated to Go’s garbage collector, which is fine and expected at this level.

---

**6. Code Generation**
In your project, **evaluation is code generation**.

Handled by:

* `evaluator/evaluator.go`

Instead of generating bytecode or assembly, you directly execute the AST and produce runtime values (`object.Object`). This makes your project an **interpreter**, not a compiler.

---

**7. Code Optimization (Machine-dependent)**
**Not present.**

This phase only makes sense if you target a machine (assembly, bytecode, VM). Since you interpret directly, there’s nothing machine-dependent to optimize.

---

**8. Info Table Management**
Handled by:

* `object/environment.go`
* `object/object.go`

This is your symbol table:

* identifiers → values
* scope chaining
* runtime bindings

Clean, minimal, and correct.

---

**9. Error Handling**
Handled across multiple layers:

* `lexer` → invalid characters
* `parser` → syntax errors
* `evaluator` → semantic/runtime errors
* `repl/repl.go` → user-facing error reporting
