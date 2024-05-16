---
tags:
---
# Cargo Workspace
cargo workspace is a feature that you can use to split a big project into multiple packages.
A _workspace_ is a set of packages that share the same cargo lock file and output directory (the target file) all cargos in the workspace also share the same target directory, as the crates within the workspace is supposed to depend on each other.
This is NOT to say cargo immediately assumes all crates within the workspace depend on each other.

## Dependency in workspace
say we have a project like this:
```
add
	- adder: the main binary
		- Cargo.toml
	- add_one: a library crate with add_one function
		- Cargo.toml
	- add_two: a library crate with add_two function
		- Cargo.toml

	- Cargo.toml
	- Cargo.lock
	- target/
```
we can see each crate within the workspace has their own TOML, but they all share the same lock file which resides at the root level. This is to ensure all crates within the workspace use the same version of a package.

As mentioned before, Cargo does NOT assume all crates depend on the native packages. That means to use a module/package in another crate we need to explicitly add it as a dependency in the TOML file.

For example, we want to let adder use a function in ```add_one```. Then, in the TOML file, we must add:
``` toml
[dependencies] 
add_one = {path = "../add_one"}
```
we can now use it in the main binary:

``` rust
use add_one
fn main() {
	let x: i32 = 10;
	println!("this is a test: {}", add_one::add_one(x));
}
```

## Running and testing packages
```cargo build```: Build the entire workspace.
```cargo run```: run the workspace as a whole.
```cargo test```: test all possible tests within the workspace
```cargo run -p [name]```: run a specific package within the workspace.
```cargo test -p [name]```: test a specific package within the workspace

## Resolver
Using the ```add``` workspace example above, when we first make the directory, add members (native packages) ONLY then do ```cargo build``` we will get this warning:

```
warning: virtual workspace defaulting to `resolver = "1"` despite one or more workspace members being on edition 2021 which implies `resolver = "2"`
note: to keep the current resolver, specify `workspace.resolver = "1"` in the workspace root's manifest
note: to use the edition 2021 resolver, specify `workspace.resolver = "2"` in the workspace root's manifest
note: for more details see https://doc.rust-lang.org/cargo/reference/resolver.html#resolver-versions
note: see more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html
```

So a warning about something called a resolver. This is to put it simply ().
To solve the warning, we can simply annotate the resolver version like so:

``` toml
[workspace]
resolver = "2"

members = [
	"subtract_one"
]
```



---
Categories: [[Cargo]]
References:
Created: 2024-05-16
