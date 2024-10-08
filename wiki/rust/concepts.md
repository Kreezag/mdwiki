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

Closure may be defined as variable but may be called as function:
```rust
let add_one = |x| x + 1;
let five = add_one(4);
```

Closures types

`FnOnce` - consumes the variables it captures from its enclosing scope, known as the closure’s environment.

`unwrap_or_else` realized with `FnOnce`:
```rust
impl<T> Option<T> {
    pub fn unwrap_or_else<F>(self, f: F) -> T
    where
        F: FnOnce() -> T
    {
        match self {
            Some(x) => x,
            None => f(),
        }
    }
}
```

`FnMut` - can change the environment because it mutably borrows values.

`sort_by_key` realized with `FnMut`:

```rust
pub fn sort_by_key<T, F, K>(slice: &mut [T], key_fn: F)
where
    F: FnMut(&T) -> K,
    K: Key,
```




