# Rust

[◀ Back](../index.md)

[Data Types](./types)

[Concepts](./concepts.md)


## Documentation

- [The Rust Programming Language](https://doc.rust-lang.org/book/)
 

## Run and build

`rustc` - tool to compile project 
  
`cargo` - build tool and package manager

`cargo new`  - create app template
`cargo build` - not optimized build + debug
`cargo run` - compile and run code
`cargo check` - build without execution
`cargo build --release` - compile with optimisation

`cargo add {package}` - install dependency

`cargo test` - run tests




## Variables

`let x` - declare immutable vars
`let mut x` - declare mutable vars
`const MY_CONST` - declare constant (always required type annotation)

we can use shadowed vars: 

    let x = 1
    …
    let x = 2	


## In code testing

`#[cfg(test)]` - attribute to indicate that the code is only used during testing
`#[test]` - attribute to indicate that the function is a test function

`assert_eq!` - macro to compare two values
`assert!` - macro to check if the value is true
`assert_ne!` - macro to check if two values are not equal

`assert!(value.is_err())` - check if the result is an error of Type Result<T, E>

`#[should_panic]` - attribute to indicate that the test should panic

`#[ignore]` - attribute to ignore the test



```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(1, 2), 3);
    }
}
```

```rust
pub struct Guess {
    value: i32,
}

impl Guess {
    pub fn new(value: i32) -> Guess {
    if value < 1 || value > 100 {
        panic!("Guess value must be between 1 and 100, got {value}.");
    }

        Guess { value }
    }
}

#[cfg(test)]
mod tests {
use super::*;

    #[test]
    #[should_panic]
    fn greater_than_100() {
        Guess::new(200);
    }
}
```
