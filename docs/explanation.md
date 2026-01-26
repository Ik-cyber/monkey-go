**Structure Explanation**

---

**1. Lexical Analysis**
Handled by:

* `token/token.go`
* `lexer/lexer.go`

This is my scanner. Raw source code goes in, and I get a stream of tokens out.
Keywords, identifiers, integers, operators, and delimiters are all produced here.

---

**2. Syntax Analysis**
Handled by:

* `parser/parser.go`
* `ast/ast.go`

The parser consumes tokens and produces an AST (Abstract Syntax Tree).
My Pratt parsing notes make this a precedence-aware expression parser.

---

**3. Semantic Analysis**
Handled by:

* `evaluator/evaluator.go`
* `object/object.go`
* `object/environment.go`

I don’t have a separate semantic analysis pass like a classical compiler. Instead, semantics are enforced during evaluation:

* Undefined variables → detected via `Environment`
* Type mismatches → detected during evaluation
* Invalid operations → runtime semantic errors

This is normal for an interpreter.

---

**4. Code Optimization (Machine-independent)**
**Not present (explicitly).**

I don’t have an optimization pass like:

* constant folding
* dead code elimination
* algebraic simplification

Some implicit optimization may occur if evaluation short-circuits expressions, but that’s incidental, not a designed phase.

---

**5. Storage Allocation**
Handled by:

* `object/environment.go`
* Go runtime (implicitly)

Variable bindings, scopes, and lifetimes are all managed by `Environment`.
Memory allocation itself is handled by Go’s garbage collector.

---

**6. Code Generation**
In my project, **evaluation is code generation**.

Handled by:

* `evaluator/evaluator.go`

Instead of generating bytecode or assembly, I directly execute the AST and produce runtime values (`object.Object`). This makes my project an **interpreter**, not a compiler.

---

**7. Code Optimization (Machine-dependent)**
**Not present.**

This phase only makes sense if I target a machine (assembly, bytecode, VM). Since I interpret directly, there’s nothing machine-dependent to optimize.

---

**8. Info Table Management**
Handled by:

* `object/environment.go`
* `object/object.go`

This is my symbol table:

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
