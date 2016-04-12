# Tail Recursion

```
def factorial(n: Int): Int = {
  @annotation.tailrec
  def go(n: Int, acc: Int): Int =
    if (n <= 0) acc
    else go(n-1, n*acc)
    
  go(n, 1)
}
```

Several things to pay attention:

* In *Scala*, a helper function is often called `go` or `loop`.
* An inner function is common in *Scala*, they are just like local variables.
* Tail recursion means the tail call does nothing but return the value of the recursive call. `go(n-1, n*acc)` returns the value of the call directly. `1 + go(n-1, n*acc)` is not.
* The `tailrec` annotation give us compile error if *Scala* is unable to eliminate the tail calls.
