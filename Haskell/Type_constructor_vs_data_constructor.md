# Type Constructors vs. Data Constructors

* A data constructor is a "function" that takes zero or more values and gives back a new value.
* A type constructor is a "function" that takes zero or more types and gives you back a new type.

```haskell
data Maybe a = Nothing
             | Just a
```

`Maybe` is a type constructor that returns a concrete type. `Just` is a data constructor that returns a value. `Nothing` is a data constructor that contains a value.


