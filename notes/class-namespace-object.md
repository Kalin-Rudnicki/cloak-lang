
Functions in a class get inherited, and can be overriden.

This allows you do define a function in a trait, and do something like:

```cloak
    function wrap[C <: Context[_], T](t: T): C[T] =
        C.wrap(t)
```

```cloak
    trait Context[T] {
        function wrap(t: T): this.type[T] // The this.type thing needs to be worked out
    }
```

And then based on the function infix rule, you could:

```cloak
    ex: MyContext[Int] = 5.wrap
```

this.type thing:

```cloak

trait Context[M, T] {
    function wrap(t: T): M[T]
}

trait Maybe[T] extends Context[Maybe, T] {
    @Override
    function wrap(t: T): Maybe[T] =
        Some[T](t)
}

```

```cloak
    def ex[A, T, C <: Context[A, T]](t: T): C[A, T] =
        C.wrap(t)
```

If a generic type is used in this way, it will be passed as a parameter

```cloak
trait Context[M][T] {
    function wrap(t: T)
}
function wrap[M <: Context[_, _]][T](t: T): M[M, T] =
    M.wrap(t)
```
