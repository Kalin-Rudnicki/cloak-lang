
# OO

Unchecked
```scala
    object Ex1 {
        def mySub(i1: Int, i2: Int): Int =
            if (i2 == 0)
                throw Sub0Err()
            else
                i1 - i2
    }

    def test1: Int =
        Ex1.mySub(5, 0)
```

Checked
```java
    class Ex2 {
        public static int mySub(int i1, int i2) throws Sub0Err {
            if (i2 == 0) {
                throw new Sub0Err();
            }
            return i1 - i2;
        }
    }

    public static int test2() throws Sub0Err {
        return Ex2.mySub(5, 0);
    }
```


# FP

Option
```scala
    object Ex3 {
        def mySub(i1: Int, i2: Int): Option[Int] =
            if (i2 == 0)
                None
            else
                Some(i1 - i2)
    }

    def test3: Option[Int] =
        Ex3.mySub(5, 0)
```

Either
```scala
    object Ex4 {
        def mySub(i1: Int, i2: Int): Either[String, Int] =
            if (i2 == 0)
                Left("Sub0Err")
            else
                Right(i1 - i2)
    }

    def test4: Either[String, Int] =
        Ex4.mySub(5, 0)
```

---

# Cloak

Errors
```scala
    namespace Ex5 {
        function mySub(i1: Int, i2: Int): Int? =
            if (i2 == 0)
                throw Sub0Err()
            else
                i1 - i2
    }

    def test5: Int? =
        Ex5.mySub(5, 0)
```

Error "cloaking"
```scala
    function test6_1: Int? =
        Ex5.mySub(5, 0) + Ex5.mySub(5, 0)

    function test6_2: Int? =
        res1: Int? = Ex5.mySub(5, 0)
        res2: Int? = Ex5.mySub(5, 0)
        res1 + res2
    
    // Whats going on under the covers?
    function test6_3: MaybeError[?, Int] =
        (~Ex5.mySub(5. 0)).flatMap(r1 =>
            (~Ex5.mySub(5, 0)).flatMap(r2 =>
                r1 + r2
            )
        )
```
```scala
    function uselessReturn5: Int? = {
        propagate ~Ex5.mySub(5, 0) // You cant hide from me
        5
    }
```
```scala
    function mySubOr0(i1: Int, i2: Int): Int =
        (~Ex5.mySub(5, 0)).save(0)
    
    function mySubOrNone(i1: Int, i2: Int): Option[Int] =
        (~Ex5.mySub(5, 0)).toOption
        
    function mySubOrLeft(i1: Int, i2: Int): Either[?, Int] =
        (~Ex5.mySub(5, 0)).toEither
```