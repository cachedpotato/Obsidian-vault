---
tags:
  - NeedWork
---
# React Fragments
A functional component in React can only return one component, meaning this is not possible:
```jsx
function App() {
	return(
		<Header />
		<Footer />
	);
}
```

We can bypass this by using what's called a fragment. Fragment is denoted by `<></>` and inside we can add multiple components like so:
```jsx
function App() {
	return(
		<>
			<Header />
			<Footer />
		</>
	);
}
```


---
Categories: [[React]]
References:
