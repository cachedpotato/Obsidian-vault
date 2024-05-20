---
tags:
---
# Weak Count
To prevent reference cycles, we can incorporate what is called ```Weak<T>```. This can be made by "downgrading" the Reference Count pointer ```Rc<T>```, like so:

``` rust
use std::rc::Weak;
let a: Weak<i32> = Weak::new(5);
```
You can create a weak reference to the value within an ```Rc<T>``` by "downgrading":
``` rust
let n: Rc<i32> = Rc::new(3);
let b: Weak<i32> = Rc::downgrade(&n);
```
Weak links _Does NOT increase strong count, but instead increases weak count_. There is also one unique property of this reference: weak counts don't need to be 0 for ```Rc<T>``` instance to be cleaned up, meaning, ```Weak<T>``` can _point to some instance that no longer exist_. This can be check using the "upgrade" method, which returns an ```Option<Rc<T>>```.

## Example: Node
**Here comes the tree train...**
``` rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug)]
struct Node {
	value: i32,
	parent: RefCell<Weak<Node>>,
	children: RefCell<Vec<Rc<Node>>>,
}
```
let's go with the fields first:
- value: the value the node holds

- parent: parent of given node. reason why we're giving it a ```Weak``` node is because if we give it a strong node, because that will make a cyclic reference between parent and child, it will cause memory leak. Parents may change, so we want internal mutability, hence the ```RefCell```

- children: child nodes. Because there can be multiple, it should be contained within a vector. and because there can be multiple connections that affect the node, we want it to have multiple ownerships, hence the ```Rc```. Finally, because we want to be able to change the children nodes within an immutable reference, We will wrap it with ```RefCell```. 

Now, lets see how strong/weak counts are created and destroyed.
``` rust
let leaf = Rc::new(Node {
	value: 5,
	parent: RefCell::new(Weak::new()),
	children: RefCell::new(vec![]),
})

println!(
	"leaf strong = {}, weak {}",
	Rc::strong_count(&leaf),
	Rc::weak_count(&leaf), //damn dangling commas are possible
);

{
	let branch = Rc::new(Node {
		value: 10,
		parent: RefCell::new(Weak::new()),
		children: RefCell::new(vec![]),
	})
	*leaf.parent.borrow_mut() = Rc::downgrade(&branch);
	
	println!(
		"leaf strong = {}, weak {}",
		Rc::strong_count(&leaf),
		Rc::weak_count(&leaf),
	);
	println!(
		"branch strong = {}, weak {}",
		Rc::strong_count(&branch),
		Rc::weak_count(&branch),
	);
}

println!("leaf parent: {:?}", leaf.parent.borrow().upgrade());
println!(
	"leaf strong = {}, weak {}",
	Rc::strong_count(&leaf),
	Rc::weak_count(&leaf),
);
```
Result:
```
leaf strong = 1, weak = 0
branch strong = 1, weak = 1
leaf strong = 2, weak = 0
leaf parent = None
leaf strong = 1, weak = 0
```
As explained above, we can find whether a weak link still exists or not with the ```upgrade``` command.

What if we printed the nodes?
```
leaf node: Node { value: 3, parent: RefCell { value: (Weak) }, children: RefCell { value: [] } }
branch node: Node { value: 5, parent: RefCell { value: (Weak) }, children: RefCell { value: [Node { value: 3, parent: RefCell { value: (Weak) }, children: RefCell { value: [] } }] } }
```
As we can see, the parent Node's value is not shown, but instead replaced with ```(Weak)```, to avoid infinite cycle.



---
Categories: [[Rc]]
References:
Created: 2024-05-20
