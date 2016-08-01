# Basic
* Functions are called by writing the function name, a space and then the parameters. `succ 8`
* Infix function can use backticks: ```92 `div` 10```
* Functions in Haskell don't have to be in any particular order. You don't have to define a function first before using it.
* In the `if` statement, the `else` part is mandatory. And the `if` statement is an *expression*. An expression is basically a piece of code that returns a value. That's why the `else` part is mandatory, since you must return something.

# Type
* A type class is a sort of interface that defines some behavior.

# Higher order functions
* Every function in Haskell is a curried function. They takes only one parameter.
* Curried functions can give you **partially applied** function.
* No matter how many times you map and filter a list, it will only pass over the list once thanks to Haskell's laziness.
* Types that can act like a box and implements `fmap` is a functor. `fmap :: (a -> b) -> f a -> f b`. It takes a function from one type to another and a functor applied with one type and returns a functor applied with another type.
* `map` is just a `fmap` that works only on lists.
* You will get `Int :: *` if you type `:k Int`. `:k` examine the kind of a type, `*` means that the type is a concrete type.
* **A concrete type** is a type that doesn't take any type parameters and values can only have types that are concrete types.
* `return` in Haskell is nothing like the `return` in most other languages. In Haskell (in I/O actions specifically), it makes an I/O action out of a pure value. Like taking a value an wraps it up in a box. It is the opposite of `<-`. `a <- return "HAHAHA"` gives you `"HAHAHA"`.
* I/O actions are values much like any other value in Haskell. We can pass them as parameters to functions and function s can return I/O actions as results. What's special about them is that if they fall into the `main` function, they are performed. So think of functions like `putStrLn` as a function that takes a string and returns an I/O action.
* Pure functions are lazy by default, which means that we don't know when they will be evaluated and  it really shouldn't matter. However, once pure functions start throwing exceptions, it matters when they are evaluated. That's why we can only catch exceptions thrown from pure functions in the I/O part of our code. Since we want to keep the I/O part as small as possible, the solution is taking advantage of Haskell's powerful type system and use types like `Either` and `Maybe` to represent results that may have failed.
* **Functors** are things that can be mapped over. In Haskell, they're described by the typeclass `Functor`, which has only one typeclass method `fmap`
* If a type constructor takes two parameters, like `Either`, we have to partially apply the type constructor until it only takes one type parameter.
* Functor laws:
	* `fmap id = id`
	* `fmap (f . g) = fmap f . fmap g`
* **Applicative Functors** is beefed up functors. First, you can do `fmap (*) (Just 3)`, what you get is `Just ((*) 3)`. So basically we get a function wrapped in a `Just`. What we want to do is mapping the function inside of a functor over another functor. This cannot be achieved by using `fmap` in functors. What we need is `Applicative`, which has two methods, `pure` and `<*>`:
	
	```
	class (Functor f) => Applicative f where
		pure :: a -> f a
		(<*>) :: f (a -> b) -> f a -> f b
	```
The class constraint says that an `Applicative` must first be a `Functor`, which means we can use `fmap` on it.
The `<*>` function takes a functor that has a function in it and another functor and sort of extracts that function from the first functor and then maps it over the second one.
* List comprehensions are just syntactic sugar for using lists as monads.
* List packages `stack exec ghc-pkg list`
* In Haskell, `where` is more common than `let`, because using `where` allows the programmer to get right to the point in defining what a function does, instead of setting up lots of local variables first.

