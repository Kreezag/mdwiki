# Rust Tips and Tricks

[◀ Back](./index.md)

---

## Error handling

To handle errors we can use `Result<T, E>` type

```rust
fn main() {
    let result = read_file("file.txt");
    match result {
        Ok(content) => println!("File content: {}", content),
        Err(error) => println!("Error: {}", error),
    }
}
```

To propagate errors we can use `?` operator

```rust
fn main() -> Result<(), Box<dyn Error>> {
    let content = read_file("file.txt")?;
    println!("File content: {}", content);
    Ok(())
}
```

To create custom error types we can use `enum` type

```rust
enum MyError {
    IoError(io::Error),
    ParseError(ParseIntError),
}

impl From<io::Error> for MyError {
    fn from(error: io::Error) -> Self {
        MyError::IoError(error)
    }
}

impl From<ParseIntError> for MyError {
    fn from(error: ParseIntError) -> Self {
        MyError::ParseError(error)
    }
}

fn main() -> Result<(), MyError> {
    let content = read_file("file.txt")?;
    let number = content.parse::<i32>()?;
    println!("Number: {}", number);
    Ok(())
}
```

To unwrap the result we can use `unwrap()` method

```rust
fn main() {
    let content = read_file("file.txt").unwrap();
    println!("File content: {}", content);
}
```

### Error handling validation

To validate that errors handles correctly we can use `#![deny(**)]` attribute

Examples:

`#![deny(clippy:unwrap_used)]`

```rust
fn main() {
    let content = read_file("file.txt").unwrap();
    println!("File content: {}", content);
}
```

`#![deny(clippy::expect_used)]` make sure that using `expect` method is not allowed

```rust
fn main() {
    let content = read_file("file.txt").expect("File not found");
    println!("File content: {}", content);
}
```

---

`#![deny(clippy::panic)]` make sure that using `panic` method is not allowed

Code will throw an error:

```rust
fn main() {
    let content = read_file("file.txt").unwrap_or_else(|error| {
        panic!("Error: {}", error);
    });
    println!("File content: {}", content);
}
```

Correct using:

```rust
fn main() {
    let content = read_file("file.txt").unwrap_or_else(|error| {
        println!("Error: {}", error);
        std::process::exit(1);
    });
    println!("File content: {}", content);
}
```

---

`#![deny(unused_must_use)]` make sure that using `Result` type is not ignored

This code will throw an error

```rust
fn read_file(file: &str) -> Result<(), io::Error> {
    fs::read_to_string(file);
}

fn main() {
    read_file("file.txt");   
}
```

Correct using

```rust
fn read_file(file: &str) -> Result<(), io::Error> {
    fs
        .read_to_string(file)
        .map(|content| println!("File content: {}", content))
}
```

