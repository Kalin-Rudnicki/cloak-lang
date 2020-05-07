
---

Exception
```scala
object SubEx1 {
    def mySub(i1: Int, i2: Int): Int =
        if (i2 == 0)
            throw new Sub0Err()
        else
            i1 - i2
}
```

Option
```scala
object SubEx2 {
    def mySub(i1: Int, i2: Int): Option[Int] =
        if (i2 == 0)
            None
        else
            Some(i1 - i2)
}
```

Usage
```scala

```

---


