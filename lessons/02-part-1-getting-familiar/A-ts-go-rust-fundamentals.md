---
description: "Let me borrow that for a moment"
---

## The fundamentals of the languages.
We are going to go over some fundamentals of each language to hopefully make
the transitioning easier.

<br />

Remember, this is fast paced, but there is room for questions.

<br />

We are not going over language specific or syntax.  So if you do have a
question, speak up during those times and I'll go over anything specific.  But
the goal here is to make a course that is geared towards people who feel
comfortable with programming and would like to pick up a second or third
language.

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Rust Borrow Checker

Rust is famous for difficulty.  For its borrow checker.  There are memes and I
personally have rage quit using rust because I didn't understand the basics of
rust.

From the rearview mirror, this is simple

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

## Lets start with other programming languages

### JavaScript
```javascript
const a = [];
const b = a;
b.push(5);
console.log(a);
console.log(b);
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### C++
```cpp
std::vector<int> a;
std::vector<int> b = a;
b.push_back(5);

printf("a size: %zu\n", a.size());
printf("b size: %zu\n", b.size());
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Rust
```rust
let a: Vec<i32> = vec![];
let mut b = a;
b.push(5);

println!("a size: {}", a.len());
println!("b size: {}", b.len());
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

## The three types
* Value
* Reference
* Mutable Reference

### The three simple rules
#### Rule #1: Value
Only one var can the value at a time.

##### Note
If the object implements copy, it can be implicitly copied

```rust
let x = 5;
let y = x;

println!("{}", x + y);
```

#### Rule #1: Reference
You can have as many references as you like with the constraint that there are
no mutable references alive.

```rust
let x = 5;
let y = &x;

println!("here is {} and {}", x, y);
```

#### Mut Reference
You can have one mut reference and no reference at the same time.

![Mutable Reference Error](./images/mut-ref-error.png)

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Moar things to cover
* Rust + Enums
* Error Handling
* Testing

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Options
Options are like nullable values

* First, lets look at it in TypeScript

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### What the code looks like

```typescript
type Foo = {
    bar?: number;
}

function test(foo: Foo) {
    if (typeof foo === undefined) { // this is annoying, yes
        // dang
    } else {
        // Undang
    }
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Lets play around with rust!

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Potential code for options

```rust
struct Foo {
    bar: Option<i32>
}

fn main() {
    let foo = Foo {
        bar: None
    };

    let foo2 = Foo {
        bar: Some(2)
    };

    if foo.bar.is_some() {
        let sum = foo.bar.unwrap() + 5;
    }

    foo.bar.unwrap_or(0);

    foo.bar.unwrap_or_else(|| {
        return 5;
    });

    let out = foo.bar.map(|x| {
        return x + 5;
    });
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### But what is an Option?
Here is the best part about rust.  You can create that type.

Lets talk about enums!

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Example of enum in TS

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

```typescript
enum Thing {
    Foo = "Foo",
    Bar = "Bar",
    Baz = "Baz"
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Lets do it in rust!

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### What my code should of approximately looked like

```rust
enum Option2 {
    Baz,
    Foo(isize),
    Bar(String),
    Fuzz(Vec<String>), // string[], or a []string
}

fn main() {
    let opt2 = Option2::Foo(5);

    let mut opt22 = Option2::Fuzz(vec![]);

    if let Option2::Foo(x) = opt2 {
        let _ = x + 5;
        // x = 7;
    }

    if let Option2::Fuzz(vec) = &mut opt22 {
        vec.push(String::from("Hello, world!"));
    }


    match opt2 {
        Option2::Baz => todo!(),
        Option2::Foo(_) => todo!(),
        Option2::Bar(_) => todo!(),
        Option2::Fuzz(_) => todo!(),
    }
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Questions so far?

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### So I said we will implement Option
So lets do it!

This will involve generics, if you are not familiar, that is ok.

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Results of this

```rust
enum Option2<T> {
    None,
    Some(T)
}

impl<T> Option2<T> {
    pub fn map(&self, f: fn(&T) -> T) -> Option2<T> {
        return match self {
            Option2::None => Option2::None,
            Option2::Some(v) => Option2::Some(f(v)),
        }
    }

    pub fn is_some(&self) -> bool {
        return match self {
            Option2::None => false,
            Option2::Some(_) => true,
        }
    }
}

fn main() {
    let opt = Some(5);
    let opt2 = Option2::Some(5);

    opt.map(|x| x + 5);
    let opt2 = opt2.map(|x| x + 5);

    if opt2.is_some() {

    }
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Questions?  That was pretty radical section
Hopefully you can see the incredible value of sumtypes.

There is this concept in 1984 that peoples ability to think is directly tied
with the language they communicate with.  I think this is true in programming
as well.  This is one of the reasons learning a ton of languages is REALLY
beneficial.

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### What about error handling?

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### TypeScript
2 types of errors that you will run across.

1. returned errors
1. thrown errors

Pretty classic typescript conflation issues (null vs undefined).  (Explain me)

Lets go over an example!

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Code

```typescript
function foo() {
    throw new Error("Goodbye, World");
}

try {
    foo();
} catch (e) {
    console.log("We had a problem, but we are ok", e);
}

console.log("great success()");
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Lets look at Go
We haven't done much of go, but it does differ here from typescript.

This is one of the most fundamental arguments against go is its error handling.
I will say that the error handling i find better than typescript but definitely
more boilerplate to deal with it.

The reason why i like it is because of control flow and where things can go
wrong.

#### Example time!
Remember, errors are just values

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### The go code
```go
package main

import (
	"errors"
	"fmt"
)

func example() error {
    return fmt.Errorf("here is an error with a string");
}

func otherExample() error {
    return errors.New("here is an error, but with errors") // approx same thing
}


// errors are pointers under the hood, so you can return the empty type
func exampleNoError() error {
    return nil;
}

type Thing struct { }

func exampleWithData(should bool) (*Thing, error) {
    if should {
        return &Thing{}, nil
    }
    return nil, fmt.Errorf("nice try, guy")
}

func main() {
    err := example();
    if err != nil {
        // handle error
    }

    _, err = exampleWithData(true)
    if err != nil {
        // handle error
    }
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Rust
Remember those enums (sumtypes)?  Its also how errors are handled.

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### The code I wrote on a sunday morning
I am sure there is a Johnny Cash reference somewhere around here.

```rust
fn error(num: i32) -> Result<(), usize> {
    if num < 0 {
        return Err((num * -1) as usize);
    }

    return Ok(());
}

fn main() -> Result<(), usize> {
    let res = error(5);

    if res.is_ok() {
        //...
    }

    let x = res.unwrap_or(());
    let x = res.expect("THIS BETTER EXIST");
    let x = res.unwrap(); // BAD

    let x = res?;

    return Ok(());
}
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Unit Testing!

* TypeScript : Cries in Configuration
* GoLang : Meh
* Rust : oyes

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

```bash
src/__tests__/test.ts
```

```typescript
test("foo", function() {
    expect("foo").toEqual("foo");
});
```

```bash
yarn add jest ts-jest @types/jest
npx jest
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Go version
there is some contention with how / where to put your tests.

* test public interfaces only
* test within the package

```
pkg/name/file.go
pkg/name/file_test.go
```

```
package name_test

import "testing"

func TestThisFunc(t *testing.T) {
    this := 5
    if this != 7 {
        t.Errorf("expected %v to equal 7", this)
    }
}
```

```bash
go test ./...
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### Rust Version
Rust, of course, is the best

* test in file

```
... // code ...

#[cfg(test)]
mod test {
    #[test]
    fn this_test() {
        assert_eq!(5, 7);
    }
}
```

```bash
cargo test
```

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />

### You will forget everything i just said
That is ok.  The best way to make it set?  Build it.

<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
