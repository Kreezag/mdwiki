# Rust Concepts

[◀ Back](./index.md)

---

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

Closures in Rust are used structures:

```rust
let x = 4;

let add_x = |num: i32 | x + num;
```

compiles to:

```rust
struct _AddX_ {
    x: i32,
}

fn _add_x_(state: _AddX_, num: i32) -> i32 {
    state.x + num
}
```

result: 

```rust
let x = 4;

let state = _AddX_ { x };

let result = _add_x_(state, 1);
```

Example of Rust closures implementation: 

FnOnce FnMut Fn - are traits that are implemented by closures

```rust
pub trait FnOnce<Args> {
    type Output;
    extern "rust-call" 
    fn call_once(self, args: Args) -> Self::Output;
}

pub trait FnMut<Args>: FnOnce<Args> {
    extern "rust-call" 
    fn call_mut(&mut self, args: Args) -> Self::Output;
}

pub trait Fn<Args>: FnMut<Args> {
    extern "rust-call" 
    fn call(&self, args: Args) -> Self::Output;
}
```

where `self`/`&mut self`/`&self` is a state of the closure are used.


## Iterators

Iterators is lazy

`iter` - iterator for immutable references
`iter_mut` - iterator for mutable references 
`into_iter` - iterator that takes ownership of the collection

Example: 

```rust
let v1 = vec![1, 2, 3];

let v1_iter = v1.iter();

for val in v1_iter {
    println!("Got: {val}");
}
```

All iterators implement trait method

```rust
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;

    // methods with default implementations elided
}
```

## Smart pointers `Box<T>`

Smart pointers - data structures that act like pointers but have additional metadata and capabilities.
Smart pointers allow data to be stored on the heap rather than the stack and have multiple data owners (reference counting).

Most common smart pointers:

`Box<T>` for allocating values on the heap

`Rc<T>`, a reference counting type that enables multiple ownership

`Ref<T>` and `RefMut<T>`, accessed through `RefCell<T>`, a type that enforces the borrowing rules at runtime instead of compile time`
