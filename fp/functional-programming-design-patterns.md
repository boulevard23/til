# Notes for Functional Programming Design Patterns
This is from a talk presented by *Scott Wlaschin*. The talk video is [here](https://www.youtube.com/watch?v=E8I19uA-wGY).

## Type

### What Is A Type
Type is just a name given to a set of values. Types are the data, they don't have any behaviors.

### Data Behavior Separation
Functions actually define the behaviors. So types separate data from behavior.

### Type Composition
Types can be composited too. There are types called **Algebraic Types**, they are not OO type system.
You can composite Algebraic Types by using 2 ways:
* Product types
* Sum types

### Totality
`Divide(): int -> int` function throws exception when divide by 0
This is not good since it lies on the function input output type. `int -> int` doesn't imply anything about the exception.

2 ways to solve that by using types:
* **Constrain** the input. Create a new type called `NonZeroInteger`. Now the function signature is `NonZeroInteger -> int`
* **Extend** the output. Create an `Option[int]`. So it will be `int -> Option[int]`

## Function

### Parameterize All The Things
You can parameterize the data input, constrains, even actions

### Function Types Are "Interfaces"
In OO, you program to the interface instead of the implementation. In FP, you program to the function type, not to the implementations.

Here is a great example:
	
	interface IBunchOfStuff
	{
		int doSomething(int x);
		string doSomethingElse(string x);
		void doAThirdThing(float x);
	}
	
*Single Responsibility Principle*: there's only one reason to change the class.
*Integration Segregation Principle*: don't make one interface do too many things.
If you push these two principles to the extreme:

	interface IBunchOfStuff
	{
		int doSomething(int x);
	}
	
This is exactly a function type: `type IBunchOfStuff: int -> int`
And functions with the same type are automatically compatible with this type, no need to explicitly implement this interface. e.g `add1 x = x + 2 // int -> int`

### Function Composition
Function composition can be used to replace *Strategy Pattern* and *Decorator Pattern* in OO.

### Partial Application
It is useful to map partial application to a collection.
Also very handy for Dependency Injection. You can apply the dependency later into the partial application.

### Continuations
A.k.a. *The Hollywood Principle*. Still take `divide()` as an example. You don't define the divide by zero case and the success case. Instead, you pass functions into `divide()` to handle these cases:
	
	let divide ifZero ifSuccess

Then you can use this function like a normal one 

	let good = divide 6 3
	let bad = divide 6 0
	
	
## Monads
	
### Monadic Bind
Monads can be considered as chaining continuation (not exactly the same). This is to combine the mismatched functions.

	let bind nextFunction optionInput =
		match optionInput with
		| Some s -> nextFunction s
		| None -> None

## Map
If you create your own generic type, create a "map" for it.
Actually, types has "map" are called "functors".

## Monoids

### Rules
* Rule 1 (Closure): The result of combining two things is always another one of the things.
* Rule 2 (Associativity): When combining more than two things, which pairwise combination you do first doesn't matter.
* Rule 3 (Identity element): There is a special thing called "zero" such that when you combine any thing with "zero" you get the original thing back.

Integer, float, string, they are all monoids.

These rules are also called **Monad Laws**. If you break these laws, you lose monoid benefits.

### Benefits
* Benefits for rule 1 (Closure): converts pairwise operations into operations that work on lists. e.g. `List.reduce`
* Benefits for rule 2 (Associativity): divide and conquer, and also parallelization for free. Another very important benefit is incremental accumulation. There is no need to store all the data and start from scratch every time. Intermediate data can be used later.
* Benefits for rule 3 (Identity element): provides initial value for empty or missing data. If the identity element is missing, it is called a semigroup.

So if you have a type which all the fields are monoids, then itself is a monoid.


