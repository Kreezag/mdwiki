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




## Variables

`let x` - declare immutable vars
`let mut x` - declare mutable vars
`const MY_CONST` - declare constant (always required type annotation)

we can use shadowed vars: 

    let x = 1
    …
    let x = 2	

