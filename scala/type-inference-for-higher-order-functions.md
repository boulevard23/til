# Type Inference for Higher-order Functions

```
def dropWhile[A](l: List[A], f: A => Boolean): List[A] = ???

val xs: List[Int] = List(1, 2, 3, 4, 5)
val ex1 = dropWhile(xs, (x: Int) => x < 4)
```

You have to put the `Int` type, this is an unfortunate restriction of the Scala compiler. **Haskell** and **OCaml** provide *complete* inference, meaning type annotations are almost never required.

What you can do here is using *curry* to improve the type inference.

```
def dropWhile[A](as: List[A])(f: A => Boolean): List[A] = ???

val ex2 = dropWhile(xs)(x => x < 4)
```

When a function definition contains multiple argument groups, type information flows from left to right across these argument groups.