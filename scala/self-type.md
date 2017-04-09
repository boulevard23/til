# Self-Type

```scala
trait Greeting {
	// self type
	this: Person =>
	
	def greeting() {
		println("Hello " + name)
	}
}

trait Person {
	val name = "Eric"
}

val greeter = new Greeting with Person
greeter.greeting
```

Self-type here mixes different traits. `this` refers to both `Greeting` and `Person`.

You can also mix multiple traits like this `this: Foo with Bar with Baz`

There is another way to do this by using inheritance:

```scala
trait Person {
	val name = "Eric"
}

trait Greeting extends Person {
	def greeting() {
		println("Hello " + name)
	}
}
```

No problem with this solution is obvious, `Greeting` is not a `Person`.

