---
tags:
---
# Crates.io
crates.io is a site where you can share and download package. Because the site distributes the source code, it is open source.

## Crate Documentation
When you release a package, especially a library crate, it's best of you to explain what each module/function does. Rust provides _[[Crate Documentation|Documentation Comment]]_, which can be used to generate HTML documentation. just add these to your code directly, and voila you have a site up and running that explains your code!

## Exporting a convenient public API
we can use the [[use#^494caa|pub use]] keyword to make modules/functions buried in multiple modules a lot easier to access.
``` rust
pub mod some_module {
	pub mod another_module {
		enum UsefulType {
			A(i32),
			B(String, String, String),
		}
	}
}
pub use my_crate::some_module::another_module::UsefulType;
```
with this re-exporting, users can now just call the ```UsefulType``` simply by ```use my_crate::UsefulType```. 

## Adding Metadata to a new crate
In the [[Cargo TOML]] file, you can add various metadata such as package name, version, etc. Here are some of the more often used metadata:
- name: name of the package
- version: current version. used for version control
- license: MIT, Apache-2.0, etc.
- edition: Rust edition
- description: short description of the crate

Adding it all would look something like this:
```toml
[package]
name = "guessing_game"
version = "0.1.0"
edition = "2021"
description = "a minigame where you guess a random number smaller than 100"
license = "MIT OR Apache-2.0"

[dependencies]
rand = "^0.8.5"
```

## Publishing to Crates.io
Now that you're finally ready, you can upload your crate to crates.io for everyone to see and enjoy. After setting up your crates.io account and your API token, simply run the command
```
cargo publish
```

## Publishing a new version
There will be infinitely more times when you have to update your crate rather than creating a new one. Whenever you update your version, simply change the version value in your TOML file and republish. Version value is recommended to follow the [[Vesion Control|Semantic Versioning Rule]]. The very basics is as follows:
- MAJOR version when you make _INCOMPATIBLE_ API changes
- MINOR version when you add functionality in a _backwards compatible_ manner
- PATCH version when you make backwards compatible bug fixes

## Deprecating Versions
As you keep updating/maintaining your crate, you'll reach a point where some version (often times old) is just plain bad, and newer versions are not just different but better in every way. In such cases you might want others to stop using that version. To do this, you need to ```yank``` that version from the site.
```
cargo yank --vers 1.0.1
```
to undo:
```
cargo yank --vers 1.0.1 --undo
```


---
Categories: [[Cargo]]
References:
Created: 2024-05-16
