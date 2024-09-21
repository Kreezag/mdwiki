# Rust

[◀ Back](../index.md)


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


## Data types

### Scalar types
- Integer
    - i8, i16, i32, i64, i128, (arch: isize - signed)
    - u8, u16, u32, u64, u128, (arch: usize - unsigned)
- Floating-point
    - f32 (single-precision float)
    - f64 (double-precision float)
- Boolean
    - bool
- Char / String
    - "a" - string literal
    - 'a' - char literal
### Tuple

 Tuples have a fixed length: once declared, they cannot grow or shrink in size.

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
let (x, y, z) = tup;
let x: (i32, f64, u8) = (500, 6.4, 1);
```

### Arrays
```
  let a = [1, 2, 3, 4, 5];
  let a: [i32; 5] = [1, 2, 3, 4, 5];
```
### Slices

reference to a contiguous sequence of elements in a collection
- `&` - reference
- `&mut` - mutable reference
- `&[i32]` - slice
- `&str` - string slice
- `&[i32]` - array slice
- `&[i32; 3]` - fixed-size array slice


    fn first_word(s: &String) -> &str {
        let bytes = s.as_bytes();

        for (i, &item) in bytes.iter().enumerate() {
            if item == b' ' {
                return &s[0..i];
            }
        }
    
        &s[..]
    }

### Structures 

    struct Person {
        name: String,
        age: u8,
    }


### Enums

    enum IpAddrKind {
        V4,
        V6,
    }

### Functions

    fn main () {}
    fn my_function() {}

### vectors
    
    let v = vec![100, 32, 57];
    for i in &v {
        println!("{i}");
    }

will throw error: cannot borrow `v` as mutable because it is also borrowed as immutable

    let mut v = vec![1, 2, 3, 4, 5];
    let first = &v[0];
    v.push(6);

    println!("The first element is: {first}");

#### Using vectors with enums:
    
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }
    
        let row = vec![
            SpreadsheetCell::Int(3),
            SpreadsheetCell::Text(String::from("blue")),
            SpreadsheetCell::Float(10.12),
        ];







