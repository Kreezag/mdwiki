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


## Closure

`Closures are anonymous functions that can capture variables from the scope in which they are defined.`

```rust
fn  add_one_v1   (x: u32) -> u32 { x + 1 } // function
let add_one_v2 = |x: u32| -> u32 { x + 1 }; // full type closure
let add_one_v3 = |x|             { x + 1 }; // no types annotation closure
let add_one_v4 = |x|               x + 1  ; // no braces closure
```



