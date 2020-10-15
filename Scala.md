
Programming in Scala, Fourth Editio


In Scala a function value  is an object.  Function types are classes that can be inherited by subclasses.


‘if’ expressions always return a result.

expression-oriented programming, or EOP
```scala
val minValue = if (a < b) a else b
```

expressions and statements

```scala
val doubledNums = for (n <- Seq(1,2,3)) yield n * 2
```

The code after the yield expression can be as long as necessary to solve the current problem.

match Expressions
```scala
val monthName = i match {
    case 1  => "January"
    case 2  => "February"
    case 3  => "March"
    case 4  => "April"
    case 5  => "May"
    case 6  => "June"
    case 7  => "July"
    case 8  => "August"
    case 9  => "September"
    case 10 => "October"
    case 11 => "November"
    case 12 => "December"
    case _  => "Invalid month"
}

count match {
    case 1 => {
        println("one, a lonely number")
    }
    case x if x == 2 || x == 3 => {
        println("two's company, three's a crowd")
    }
    case x if x > 3 => {
        println("4+, that's a party")
    }
    case _ => {
        println("i'm guessing your number is zero or less")
    }
}
```
