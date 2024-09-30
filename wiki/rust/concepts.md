# Rust Concepts


## Ownership
`Rust has a unique approach to memory management: it's ownership system. It's a set of rules that the compiler checks at compile time. It's a way to manage memory without a garbage collector.`

## Monomorphization
`Monomorphization is the process of turning generic code into specific code by filling in the concrete types that are used when compiled.`


## Lifetime 
`Lifetime is a way to tell the compiler how long references are valid. It's a way to prevent dangling references.`

Lifetime Annotation Syntax:
```rust
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```
