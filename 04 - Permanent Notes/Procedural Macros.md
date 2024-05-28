---
tags:
---
# Procedural Macros
Whereas declarative macros use pattern matching to convert one code to another code, procedural macros act a lot like a function: it receives code as input, operates on it, then outputs a code. As mentioned, procedural macros can be further divided into three types: custom derive macros, attribute macros, and functional macros.
## Custom Derive Macros
derive macros are essentially macros that bypasses the `impl` process of traits. A good example of this is `#[derive(Debug)]`, where we implement the `Debug` trait without the need for `impl` block on a type. Hold tight, this is gonna get pretty long.
### Basic structure
the crate structure will look something like this:
```
trait_name
├── Cargo.lock
├── Cargo.toml
├── src
│   └── lib.rs
├── trait_name_derive
│   ├── Cargo.toml
│   └── src
└── target
    ├── CACHEDIR.TAG
    └── debug
```
the main `trait_name/lib.rs` contains the trait definition:
``` rust
pub trait MyTrait {
	pub fn trait_method;
}
```
inside the main `cargo.toml`, we will add `trait_name_derive` as dependency:
``` toml
[dependencies]
trait_name_derive = {path = ./trait_name_derive}
```

inside the `trait_name_derive/cargo.toml`, we will add the following:
``` toml
#--snip
[lib]
proc-macro = true
[dependencies]
syn = "2.0.0"
quote = "1.0.0"
```
- `proc-macro`: We're going to take `proc_macro::TokenStream` for the code parser, which we'll see in a minute.
- `syn`: for parsing syntax into tree that we can use for macros.
- `quote`: to make a `syn` structure back into rust code.

### Inside the `trait_name_derive/src/lib.rs`
this is where the good stuff happens. We will have two functions:
- `trait_name_derive`: the `run()` function for derive macros. In charge of parsing using `syn`
- `impl_trait_name`: where the _actual_ magic happens. This function is in charge of the actual implementation process when we use the `#[derive]` macro.

Let's take an example taken from the Rust Book.
``` rust
use proc_macro::TokenStream;
use quote::quote;
use syn;

#[proc_macro_derive(HelloMacro)]
pub fn hello_macro_derive(input: TokenStream) -> TokenStream {
	//construct a representation of rust code as syntax tree
	//that we can manipulate
	let ast = syn::parse(input).unwrap();

	//build the trait implementation
	impl_hello_macro(&ast)
}
```
This is the `trait_name_derive` part. The `ast` here is the syntax tree we get using `syn.parse()`. For a simple type structure, the syntax tree looks like this:
```
DeriveInput {
    // --snip--

    ident: Ident {
        ident: "Pancakes",
        span: #0 bytes(95..103)
    },
    data: Struct(
        DataStruct {
            struct_token: Struct,
            fields: Unit,
            semi_token: Some(
                Semi
            )
        }
    )
}
```
we can call the fields using their key names.
Now let's look at the implementation function:
``` rust
fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
	let name = &ast.ident
	let gen = quote! {
		impl HelloMacro for #name {
			fn hello_macro() {
				println!("Hello Macro! My name is {}", stringify!(#name));
			}
		}
	};
	gen.into()
}
```
we can see that we got the `ident` field which is the name of the struct using `&ast.ident`. inside the `quote!` macro we write exactly how the `impl` block would look like for a given trait, and place the `#name` for places where struct/enum names are needed. The `stringify!` macro will turn an expression, such as `1 + 2`, into a string, like `"1 + 2"`. Crazy!

Now that the macro part is done, let's actually use this thing. after `cargo build`, create a new cargo that'll use this macro, and in the TOML file we add:
``` toml
[dependencies]
trait_name = {path = "path/to/trait_name"}
trait_name_derive = {path = "path/to/trait/trait_name_derive"}
```
Finally, in the `main.rs`:
``` rust
use trait_name::MyTrait;
use trait_name_derive::MyTrait;

#[derive(MyTrait)]
struct MyStruct;
```
... Yeah all this code just to use the `derive` macro. Is it worth it? idk you decide.

## Attribute-like macros
Attribute-like macros is the same with custom derive macros, only it is more flexible and can be applied to anything, whereas custom derive macros can only be used for structs and enumerations.
``` rust
#[route(GET, "/")]
fn index() {...}
```
the `#[route]` attribute would be defined by the framework as a procedural macro, and the signature will be like the following:

```rust
#[proc_macro_attribute]
pub fn route(attr: TokenStream, item: TokenStream) -> TokenStream {...}
```
- the `attr` part is for the attribute: `GET`, `"/"`
- the `item` part is for the function: `index()`

## Function-like macros
function-like macros can take any number of arguments like declarative macros can. However, whereas `macro_rules!` macros can be defined only using the match-like syntax, function-like macros can take a `TokenStream` parameter and their definition manipulates that `TokenStream` using Rust code like other procedural macros. an example of this is `sql!`
```rust
let sql = sql!(SELECT * FROM posts WHERE id=1);
```
wait, SQL in Rust? Yeah, pretty much. This means, using macros, we can add parts of _OTHER LANGUAGES/APIS_ directly to rust code. the implementation signature would look something like this:
```rust
#[proc_macro]
pub fn sql(input: TokenStream) -> TokenStream {...}
```


---
Categories: [[Rust Macros]]
References:
Created: 2024-05-28
