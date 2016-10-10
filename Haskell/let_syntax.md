# `let` Syntax
The keyword `let` is used in three ways in Haskell

1. *let-expression:*

	```haskell
	let variable = expression in expression
	```

2. *let-statement* This form is only used inside of do-notation, and does not use `in`

	```haskell
	do statements
		let variable = expression
		statements
	```

3. Used inside of list comprehensions without `in`

	```haskell
	[(x, y) | x <- [1..3], let y =  2 * x]
	```

	You can use `let` with `in` inside of do-notation, but the indentation rules makes it kinda hard, so never use `in` in a list comprehension or a do-block.

	```haskell
	do let x = 42 in
	   foo
	```

	gets parsed as

	```haskell
	do (let x = 42 in foo)
	```

	Without indentation, you get a parse error:

	```haskell
	do (let x = 42 in)
	   foo
	```



