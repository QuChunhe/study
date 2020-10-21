
Programming in Scala, Fourth Editio


In Scala a function value  is an object.  Function types are classes that can be inherited by subclasses.

https://hello-scala.com/202-scala-list-class.html

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

In Scala, the primary constructor of a class is a combination of:
* The constructor parameters
* Methods that are called in the body of the class
* Statements and expressions that are executed in the body of the class

val makes fields read-only

You define auxiliary Scala class constructors by defining methods that are named this. There are only a few rules to know:
* Each auxiliary constructor must have a different signature (different parameter lists)
* Each constructor must call one of the previously defined constructors

Supplying Default Values for Constructor Parameters.

Named parameters

Enumerations

```scala
sealed trait DayOfWeek
case object Sunday extends DayOfWeek
case object Monday extends DayOfWeek
case object Tuesday extends DayOfWeek
case object Wednesday extends DayOfWeek
case object Thursday extends DayOfWeek
case object Friday extends DayOfWeek
case object Saturday extends DayOfWeek
```

Using Scala Traits as Interfaces

Extending multiple traits
* Use **extends** to extend the first trait
* Use **with** to extend subsequent traits

Abstract Classes

Scala traits don’t allow constructor parameters


One way I remember those method names is to think that the : character represents the side that the sequence is on, so when I use +: I know that the list needs to be on the right, like this:
```
0 +: a
```
and when I use :+ I know the list needs to be on the left:
```
a :+ 4
```

 a function that takes another function as an input parameter is known as a Higher-Order Function (HOF).
 
 Option/Some/None  Try/Success/Failure
 ```
def toInt(s: String): Option[Int] = {
    try {
        Some(Integer.parseInt(s.trim))
    } catch {
        case e: Exception => None
    }
}

toInt(x) match {
    case Some(i) => println(i)
    case None => println("That didn't work.")
}
```

```
def toInt(s: String): Try[Int] = Try {
    Integer.parseInt(s.trim)
}

toInt(x) match {
    case Success(i) => println(i)
    case Failure(s) => println(s"Failed. Reason: $s")
}
 ```
 
 A companion object in Scala is an object that’s declared in the same file as a class, and has the same name as the class. 
 
 apply  and unapply method
 
 Case Classes
* Case class constructor parameters are public val fields by default, so accessor methods are generated for each parameter.
* An **apply** method is created in the companion object of the class, so you don’t need to use the new keyword to create a new instance of the class.
* An **unapply** method is generated, which lets you use case classes in more ways in match expressions.
* A **copy** method is generated in the class. I never use this in Scala/OOP code, but I use it all the time in Scala/FP.
* **equals** and **hashCode** methods are generated, which let you compare objects and easily use them as keys in maps.
* A default **toString** method is generated, which is helpful for debugging.

the biggest advantage of case classes is that they support pattern matching.

Methods and values that aren’t associated with individual instances of a class belong in singleton objects, denoted by using the keyword **object** instead of **class**.


Case objects
* It is serializable
* It has a default **hashCode** implementation

