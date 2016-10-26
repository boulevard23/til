# What is Haskell

### Functional
* Functions are first-class. Functions are values can be used.
* Models computations as evaluating expression rather than executing instructions.

### Pure
* Expressions are always referential transparent.

### Lazy
* Expressions are evaluated until their results are actually needed.

### Statically Typed
* Type errors will not compile

# Basic
* Variables are all immutable.
* Functions are called by writing the function name, a space and then the parameters. `succ 8`
* Infix function can use backticks: ```92 `div` 10```
* Functions in Haskell don't have to be in any particular order. You don't have to define a function first before using it.
* In the `if` statement, the `else` part is mandatory. And the `if` statement is an *expression*. **An expression is basically a piece of code that always returns a value.** That's why the `else` part is mandatory, since you must return something.
* List comprehension example: `[x*2 | x <- [1..10], x*2 >= 12, odd x]`. You can apply multiple filters.
* Tuple is not *homogenous*, it can contain different types.

# Type
* Type print: `:t '4 == 5'` results `4 == 5 :: Bool`.
* `Int` has max and min number. `Integer` is not bound, it can eat all your memory.
* Type variable. `:t head` results `head :: [a] -> a`. `a` here can be any type, it's like generics in other languages. Functions have type variables are called **polymorphic functions**.
* A type class is a sort of interface that defines some behavior. Like a Java interface, only better.

	```haskell
	ghci> :t (==)
	(==) :: (Eq a) => a -> a -> Bool
	```
	`=>` is called **class constraint**. `Eq` is a type class, it provides an interface for equality check.

# Pattern Matching
* You can define multiple function bodies for different patterns
	
	```haskell
	factorial :: (Integral a) => a -> a  
	factorial 0 = 1  
	factorial n = n * factorial (n - 1)  
	```
	
* Pattern matching only works for constructors:

	```haskell
	data Foo = Bar | Baz Int
	f :: Foo -> Int
	f Bar     = 1
	f (Baz x) = x - 1
	```
	
	Here `Bar` and `Baz` are constructors for the type `Foo`.
	And `0` in previous `factorial 0 = 1` actually is a constructor for the `Integral` data type.
	
* `all@(x:y:_)`. `all` here is the whole list.
* Guides

	```haskell
	bmiTell :: (RealFloat a) => a -> a -> String  
	bmiTell weight height  
    | bmi <= 18.5 = "You're underweight, you emo, you!"  
    | bmi <= 25.0 = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= 30.0 = "You're fat! Lose some weight, fatty!"  
    | otherwise   = "You're a whale, congratulations!"  
    where bmi = weight / height ^ 2 
	```
	Guides are indicated by pipes.
* `let <bindings> in <expression>`. Difference between `let` binding and `where` binding is that, `let` returns an expression.

	```haskell
	ghci> 4 * (let a = 9 in a + 1) + 2  
	42 
	```
*	Case expression

	```haskell
	head' :: [a] -> a  
	head' xs = case xs of [] -> error "No head for empty lists!"  
                      (x:_) -> x  
	```
	

# Higher order functions
* **Curried function**:
	* Every function in Haskell is a curried function. They takes only one parameter. 
	* Curried functions can give you **partially applied** function, which is when you call a function with too few parameters. And it is beneficial because:
		* You can create functions on the fly and pass them to another function.
		* You can seed the functions with some data.
	* Good article on [Scala curried function and partially applied functions](http://www.vasinov.com/blog/on-currying-and-partial-function-application/)
	* Currying infix function by surround with parentheses and only supply a parameter on one side: `(/10)` or `(10/)`.
	* Whenever you have a function like `foo a = bar b a`, you can convert it into `foo = bar b` because of currying. And this is called **Point Free Style**.

* No matter how many times you map and filter a list, it will only pass over the list once thanks to Haskell's laziness. This is not true for Scala though :(
* **Lambdas**: 
	* They are just anonymous functions that are used because we need some functions only once.
	* E.g: `map (\x -> x + 3) [0, 1, 2, 3, 4]`
	* You can also do pattern matching: `map (\(a,b) -> a + b) [(1,2),(3,5),(6,3),(2,6),(2,5)]`
* **Fold**:
	* `foldl` folds the list from the left side. The accumulator is the first parameter:

		```haskell
		sum' :: (Num a) => [a] -> a  
		sum' xs = foldl (\acc x -> acc + x) 0 xs
		```
	* `foldr` folds the list from the right side. The accumulator is the second parameter:

	  	```haskell
	  	sum' :: (Num a) => [a] -> a
	  	sum' xs = foldr (\x acc -> x + acc) 0 xs
	  	```
	
	* Folds can be used to implement any function where you traverse a list once, element by element, and then return something based on that.
	
* **Function application**:
	
	```haskell
	f x y z
	```
  This is called an application of a function `f` to three parameters `x`, `y` and `z`.
	
	* `->` is right associative by default. But function application with a space is actually left associative
	
		```haskell
		f :: a -> b -> c
		f x y = ...
		```
		is actually
		
		```haskell
		f :: a -> (b -> c)
		(f x) y = ...
		```
	  The type definition reads as function `f` takes a parameter type of 	`a` and returns a function which takes a parameter type of `b` and returns a type of `c`.
	  And the function application reads as apply `x` to function `f` and gets another function back, then apply `y` to that function.
	* Function application with `$` is right associative. `f (x (y z))` can be written as `f $ x $ y z`

* **Function composition**:
	
	```haskell
	(.) :: (b -> c) -> (a -> b) -> a -> c  
f . g = \x -> f (g x)
	``` 
	
	* `.` is right associative.
	* You can get the point free style by using function composition:
		
		```haskell
		fn x = ceiling (negate (tan (cos (max 50 x))))
		```
		to
		
		```haskell
		fn = ceiling . negate . tan . cos . max 50
		```

# Types and Typeclasses

* **Algebraic Data Types**

	```haskell
	data Bool = True | False
	```
	
	The left part denotes the type, the right parts are **value constructors**. They specify different values that this type can have.
* **Value constructors** are actually functions accept parameters and return a value of a data type.

	```haskell
	data Shape = Circle Float Float Float | Rectangle Float Float Float Float
	```
	So here, `Circle` is a value constructor accepts 3 parameters. 
	
	* You can check the type signature of the value constructor:
	
		```haskell
		ghci > :t Circle
		Circle :: Float -> Float -> Float -> Shape
		```
	* Pattern matching against the value constructor:

		```haskell
		surface :: Shape -> Float
		surface (Circle _ _ r) = pi * r ^ 2
		surface (Rectangle x1 y1 x2 y2) = (abs $ x2 - x1) * (abs $ y2 - y1)
		```

* **Typeclasses** are like interfaces. It defines some behavior like comparing for equality, comparing for ordering, etc. A *type* that can behave in that way are made instance of a typeclass.

* To make a type extends some other typeclasses:

	```haskell
	data Point = Point Float Float deriving (Show)
	```

* **Record Syntax**, instead of using the above data definition with only the types, we can use the record syntax to assign a name to each field:

	```haskell
	data Person = Person { firstName :: String  
                     	 , lastName :: String  
                     	 , age :: Int  
                     	 } deriving (Show)   
	```
	
	By doing this, Haskell automatically makes functions: `firname`, `lastname` and `age` as getters.
	
	```haskell
	ghci > :t lastname
	lastname :: Person -> String
	```
	
	Also, we can create instances by specifying both the name and value:
	
	```haskell
	ghci > Person {lastname="Winston", firstname="Harry", age=46}
	```
	
	And the order doesn't matter.
	
* **Type constructor** can take types as parameters to produce new types

	```haskell
	data Maybe a = Nothing | Just a
	```
	
	`a` here is the type parameter. And since there is a type parameter here, we call `Maybe` a type constructor.

* *Don't put typeclass constraints in data declarations.*

	```haskell
	data (Ord k) => Map k v = ...
	```
	
	Then you will have to put the constraints into the function type declarations, even if the function actually doesn't need that declaration.

* A type can be made an **instance** of a typeclass if it supports that behavior. Example: type `Int` is an instance of the `Eq` typeclass because the `Eq` typeclass defines behavior for stuff that can be equated.
* `Bounded` and `Enum`

	```haskell
	data Day = Monday | Tuesday | Wednesday | Thursday | Friday | Saturday | Sunday   
               deriving (Eq, Ord, Show, Read, Bounded, Enum)
	```
	
	`Bounded` typeclass gives you the min and max bound:
	
	```haskell
	ghci > minBound :: Day
	Monday
	ghci > maxBound :: Day
	Sunday
	```
	
	`Enum` is for things have predecessors and successors:
	
	```haskell
	ghci > succ Monday
	Tuesday
	ghci > pred Saturday
	Friday
	ghci > [Thursday .. Sunday]
	[Thursday,Friday,Saturday,Sunday]  
	ghci> [minBound .. maxBound] :: [Day]
  [Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday]  
	```
		
* **Type synonyms** it is just a type alias for convenience:

	```haskell
	type String = [Char]
	```
	
	It can also be parameterized:
	
	```haskell
	type AssocList k v = [(k, v)]
	```
	
	`AssocList` here is a type constructor.
	
* Difference between **type constructor** and **value constructor**: `AssocList` is a type constructor, but you cannot do `AssocList [(1,2), (3,4)]` because it doesn't create a value of that type. We can do `[(1,2), (3,4)] :: AssocList Int Int`

* **Recursive data structures**: you can recursively use a type in this type's definition.

	```haskell
	data List a = Empty | Cons a (List a) deriving (Show, Read, Eq, Ord)
	```
	
* Define a typeclass

	```haskell
	class Eq a where  
      (==) :: a -> a -> Bool  
      (/=) :: a -> a -> Bool  
      x == y = not (x /= y)  
      x /= y = not (x == y)
	```
	
	* `class` is totally a different thing from Java.
	* `a` is the type variable, referring an instance of `Eq` which will be created later on.
	* The functions defined in the typeclass don't need to be implemented. But we have to specify the type declarations.
	* Create an instance of typeclass
		
		```haskell
		data TrafficLight = Red | Yellow | Green
		
		instance Eq TrafficLight where  
    		Red == Red = True  
     		Green == Green = True  
     		Yellow == Yellow = True  
     		_ == _ = False
		```
		
		We can derive the `Eq` typeclass, this is just an example to illustrate.

* Subclasses of other typeclasses

	```haskell
	class (Eq a) => Num a where
	```
	
	It means that we have to make a type an instance of `Eq` before we can make it an instance of `Num`. So a class constraint on a class declaration is **subclassing**.
	
* `:info typeclass` will give you all the functions this typeclass defines.
* Functions have type declarations, types also have these, they are called **kinds**.

	```haskell
	ghci > :k Int
	Int :: *
	ghci > :k Maybe
	Maybe :: * -> *
	ghci > :k Maybe Int
	Maybe Int :: *
	```
	
	`*` means that type is a concrete type.

# I/O

* No side-effect is actually impossible. What Haskell does is separate the pure part and the impure part. The benefit is that we can still reason about the pure part.
* Type of `putStrLn`

	```haskell
	ghci > :t putStrLn
	putStrLn :: String -> IO()
	```
	
	`putStrLn` takes a string and returns an **I/O action**.
	
* An example:

	```haskell
	main = do
		putStrLn "Hello, what's your name?"
		name <- getLine
		putStrLn ("Hello " ++ name)
	```
	
	* I/O action can only be performed in `main`
	* You can use the `do` syntax and perform several I/O actions.
	* `getLine` has the type `IO String`. `IO` is a type constructor.
	* In a `do` block, last action cannot be bound to a name. It automatically extracts the value from the last action and binds it to its own result.
	* To extract the value out of an I/O action, you have to use `<-`

* `return` in Haskell I/O actions means making an I/O action out of a pure value. When we need some I/O action to carry out an empty input line, we can use `return ()`. `return "hehe"` will have a type of `IO String`. Using `return` will not terminate the execution, it is nothing like most other languages.

# Exception

* Haskell has a very good type system. `Maybe` and `Either` is very good for failure handling. But we still need support for exceptions because they make more sense in I/O contexts. A lot of things could go wrong when dealing with the outside world since it is unreliable.
* Not only I/O code can throw exceptions. Pure code can also throw exceptions too.

	```haskell
	ghci > 4 `div` 0
	*** Exception: divide by zero
	ghci > head []
	*** Exception: Prelude.head: empty list
	```
	
* Pure code throws exceptions, but they can only be caught in the I/O part of our code (`do` block in `main`). That's because you don't know when the pure code gets evaluated since it is lazy and doesn't have a well-defined order of execution, whereas I/O code does.
* We want to catch exceptions threw from the pure code, but we also want to keep the I/O part as small as possible. The best way is to take advantage of Haskell's powerful type system and use types like `Either` and `Maybe` to handle the failures.

# Functor

* Types that can act like a box and implements `fmap` is a functor. 
	
	```haskell
	class Functor f where
		fmap :: (a -> b) -> f a -> f b
	```

	* `fmap`It takes a function from one type to another and a functor applied with one type and returns a functor applied with another type.
	* `f` is not a concrete type, but a type constructor that takes one type paramter.

* `map` is just a `fmap` that works only on lists.
		
====


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
	
	```haskell
	class (Functor f) => Applicative f where
		pure :: a -> f a
		(<*>) :: f (a -> b) -> f a -> f b
	```
The class constraint says that an `Applicative` must first be a `Functor`, which means we can use `fmap` on it.
The `<*>` function takes a functor that has a function in it and another functor and sort of extracts that function from the first functor and then maps it over the second one.
* List comprehensions are just syntactic sugar for using lists as monads.
* List packages `stack exec ghc-pkg list`
* In Haskell, `where` is more common than `let`, because using `where` allows the programmer to get right to the point in defining what a function does, instead of setting up lots of local variables first.
* Parametric polymorphism. When you write a polymorphic function, it must work for every possible input type. 

	```haskell
	notEmpty :: [a] -> Bool
	notEmpty (_:_) = True
	notEmpty _     = False
	```
	The `notEmpty` function does not care what `a` is. This is what the parametric polymorphism means. One benefit is something called *type erasure*. Because a running Haskell program can never make decisions based on type information, all the type information can be dropped during compilation. This property gives Haskell a huge speed boost when compared to other languages, such as Python, that need to keep types around at runtime.
*	*Partial function* `head` is what is known as a *partial function*. It is not defined for an empty list. Functions which have certain inputs that will make them recurse infinitely are also called partial. Functions which are well-defined on all possible inputs are known as *total functions*. Avoiding partial functions is good practice in any programming language.

