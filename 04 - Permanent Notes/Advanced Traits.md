---
tags:
---
# Advanced Traits
Here are some of the more advanced use cases of traits. 

- [[Associated Types]]
Associated types are used as a placeholder for the trait implementors to use. We've already seen an example of this with the `Iterator` trait.

- [[Default Generic Type and Operator Overloading]]
When we define a generic type, we can set the default type using `<GenericType=DefaultType>` syntax.

- [[Fully Qualified Syntax]]
There can be instances where we implement multiple traits on a type that has an identically named method. For disambiguation, we use what's called a fully qualified syntax.

- [[Supertraits]]
Supertraits are traits that implements other traits. In other words, traits with trait bounds.

- [[Newtype Patterns]]
Enums are used as a light wrapper around an external type to implement an external trait, thereby bypassing the [[Traits in Rust#^240317|Orphan Rule]]. 

---
Categories: [[Traits in Rust]]
References:
Created: 2024-05-24
