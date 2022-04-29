# Overview
Macros are meta-programming that generates code during compile time. This taking input of some pattern and producing code that fits the requirements.  Note that all macros need to utilized valid Rust syntax(ident, types, delimiters, and signs). Macros can also be in macros, whow...

## macro_rules!
Macro rules is a macro that allows you to define patterns as inputs and then generate code as output. You are basically matching on patterns and outputting code blocks
Syntax review: https://doc.rust-lang.org/rust-by-example/macros/syntax.html

**Expansion**
Defined Rust macros params, using macro_rules, support expansion of multiple arguments. They are defined via the expansion enclosure `$()`. They also support a delimiters and the number of params(using the regex like syntax of +/*/?).
https://doc.rust-lang.org/reference/macros-by-example.html

**Fragment Specification**
macro_rules support different fragments, kinda like types of inputs, for their expressions.
https://doc.rust-lang.org/reference/macros-by-example.html#metavariables

## proc_macro
Take in a series of TokenStreams, a ATS tree, or operations that a struct or impl is going to run. Then we need to returned an altered TokenStreams on how we want generate this code.
**Syn**
Is a really useful library that helps break out TokenStreams into a more manageable tree structure.

## cargo-expand
A really nice tool that will expand macros

# References
The Little Book of Rust Macros http://danielkeep.github.io/tlborm/book/README.html
Crust of Rust: Declarative Macros: https://www.youtube.com/watch?v=q6paRBbLgNw