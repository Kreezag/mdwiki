# Data Types

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


### Hash map

create

    use std::collections::HashMap;

    let mut scores = HashMap::new();

insert

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

alternative insert

    scores.entry(String::from("Yellow")).or_insert(50);
    scores.entry(String::from("Blue")).or_insert(50);

get element

    let team_name = String::from("Blue");
    let score = scores.get(&team_name).copied().unwrap_or(0);

or

    for (key, value) in &scores {
        println!("{key}: {value}");
    }


### Generics

Example of a generic function:

    struct Point<T> {
        x: T,
        y: T,
    }

    impl<T> Point<T> {
        fn x(&self) -> &T {
            &self.x
        }
    }
    
    impl<X1, Y1> Point<X1, Y1> {
        fn mixup<X2, Y2>(self, other: Point<X2, Y2>) -> Point<X1, Y2> {
            Point {
                x: self.x,
                y: other.y,
            }
        }
    }

Standard library generic example:

    Some(T) // T is a type
    Result<T, E> // T is a type, E is Error


