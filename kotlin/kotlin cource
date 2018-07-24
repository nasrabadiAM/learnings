kotlin cource 

Hadi Hariri




-_-_-_-_-_-_-_



jvm is an abstract machine, it has three parts: spesification, implementation and instances.

there is a single specification and multiple implementation(most popular implementation is OpenJDK). 

instances are the environments that each java application run on it.


we have two tools for java: JRE which is the tool for runnig jvm based applications and JDK which is the tool for develping jvm based applications.




------------------------------------

REPL and kotlinc
---

After installing kotlin compiler we can run it with 'kotlinc' command in terminal(actully it sould be added to the path).

When you run the kotlin ompiler, Actually 'REPL' runs. REPL is a tool(something like python inteprete) that runs kotlin codes interactivly.


we can use REPL in two ways:

First is with running kotlinc command in terminal

And second is whith openning Intelij idea REPL tool that is more complete and have code completion and other stuffs.

For opening REPL of intelij idea you can go to 'Tools > Kotlin > Kotlin REPL'

--------------------------------------


Top-level functions
---
We have top-level functions in kotlin that needn't any upper class to define a method. you can define a method in top-level part of a file wothout defining a calss.


Main function
---
```kotlin
 fun main(args:Array<String>()){
 		println("Hello main function")
 }
```
main function in kotlin is a specific function that is the starting point of the application.

In kotlin we can have multiple main functions per package. acually we can have a main function in each file.



Packages
---
In kotlin we have packages but when we don't specify package, it interpretes as default package.


Semicolons
---
In Kotlin we are not force to use semicolons and we can ommit it everywhere.

We can have multiple classes per file in kotlin.

Package doesn't have to match folder names.


Variables
---
var is for declaring mutable types in kotlin

```kotlin
var streetNumber: Int

var streetName: String = "High street"
//or
var streetName = "High street"
```

val is for declaring immutable or read-only types in kotlin, so we can't change its value later.

```kotlin
val zip: String = "AR"

//or 

val zip = "AR"
```

It is better to use val to provide immutablility


We have no implicit conversions in kotlin.

```kotlin
 	val myLong = 454L
    val myFloat = 45F

    val myBinary = 0xb797
    val myHex = 0x468ab

    val myInt = 45
    val myLongAgain: Long = myInt.toLong()


    // strings

    val myChar = 'A'
    val myString = "Hello"

    val escapeChars = "Hello everyBody\n"

    val rawString = "Hello everyBody " +
            " And this is the second line but not that you " +
            "think!"

    val multipleLines = """ Hello every body
        And it is the real second line
        """


    //String interpolation
    val year = 10
    val message = "the decade is $year years"

    val name = "Mary"
    val anotherMessage = "her name length is ${name.length}"
```




Any
---
is equivalent to Object in java, it is any class in kotlin.


loops
---

```kotlin
   //for-loop
    for (i: Int in 1..100) {
        println(i)
    }

    //shorter version
    for (i in 1..100) {
        println(i)
    }

    // step 3
    for (i in 1..50 step 3) {
        println(i)
    }

    // int loop downTo in step 3
    for (i in 20 downTo 200 step 3) {
        println(i)
    }

    //int loop in step 3
    for (i in 20..200 step 3) {
        println(i)
    }

    //string loop
    val capitals = listOf("Tehran", "Dameshgh", "Alley")
    for (capital in capitals) {
        println(capital)
    }

    //while
    var i = 10
    while (i > 0) {
        print(i)
        i--
    }

    //do-while
    var x = 100
    do {
        println(x)
        x %= 2
    } while (x < 0)


    //break
    loop@ for (i in 0..100) {
        for (j in 100 downTo 0) {
            if (i % j == 0)
                break@loop
        }
    }

    //continue
    for (i in 0..100) {
        for (j in 100 downTo 0) {
            if (i % j == 0)
                continue
        }
    }
```




conditions
---


```kotlin
 //simple if
    val name = "Ali"

    if (name != "") {
        println(name)
    } else {
        println("Empty")
    }


    // if statement returning a value
    val result = if (name == "") {
        20
    } else {
        30
    }
    println(result)


    //when is like switch
    val nami = "Value"
    when (nami) {
        is String -> {
            println("Is String")
            println("Another line of statement")
        }
        "Value" -> println("Is Int")
    }

    //when returning a value
    //when is like switch
    val whenResult = when (nami) {
        is String -> {
            println("Is String")
            println("Another line of statement")
        }
        "Value" -> println("Is Int")
        else -> println("oops!")
    } 
```




import
---

we can import like this:


```kotlin
import utils.someUtility as someUtilityFromUtils
```


in this way we have no conflicts between imports.




Functions
---

'Unit' in kotlin means 'void' but it has some more advantages. it is an object actually.

Nothing is a return type that we use to say that the return value never exists, like when it throws an exception.


```kotlin
fun main(args: Array<String>) {

}

fun hello(): Unit {
    println("Hello")
}

fun helloo() {
    println("Hello")
}

fun nothingReturn(): Nothing {
    throw RuntimeException("nothing returns")


}fun returnsFour(): Int {
    return 4
}

fun sum(x: Int, y: Int): Int {
    return x + y
}

fun sumShort(x: Int, y: Int): Int = x + y

fun sumVeryShort(x: Int, y: Int) = x + y


// function with default values

fun sum(x: Int, y: Int, z: Int = 0) = x + y + z



// when default value is in the middle

printDetails("Ali", phone = "+9899999")

fun printDetails(name: String, email: String = "", phone: String) {
    println("name: $name - email: $email - phone: $phone")

}


//re-order function inputs

printDetails("Ali", phone = "+9899999", email = "dasd@jfafj.cc")


//function with infinite varargs input

printNames("Ali")
printNames("Ali", "Reza")
printNames("Ali", "Reza", "Behzad")

fun printNames(vararg names: String) {
    for (name in names)
        println(name)
}



//we can pass varargs values to another method with adding * before value

fun printNames(vararg names: String) {
    printNamesSequentially(*names)
}

private fun printNamesSequentially(vararg names: String) {
    for (name in names)
        println(name)
}


```



classes
---
classes are declared with class and className and nothing else, but if we want to declare some property in the class we must use curly braces.

we have no fileds in kotlin classes, everyThing in a class is a property and functions.

we just have 'backing' fields in setters/ getters. 

```kotlin 
class Customer {
    var id: Int = 0
    var name: String = ""
}


//or
class Customer(initId: Int, initName: String) {
    var id: Int = initId
    var name: String = initName
}

//or
class Customer(var initId: Int, var initName: String) {
//
}
```

if we use var before passed items to the class constructor, we make them class properties, but if we don't, we just passed them.

```kotlin
class Customer(var initId: Int, var initName: String = "")
```

we can use init block to init some stuff, this block usually execute when class is initializing.
```kotlin
class Customer(var initId: Int, var initName: String = "") {
    init {
        initName.toUpperCase()
    }
}

```  

we can define more constructors like this

```kotlin
class Customer(var initId: Int, var initName: String = "") {
    init {
        initName = initName.toUpperCase()
    }

    var familiyyy: String = ""

    constructor(id: Int, name: String, family: String) : this(id, name) {
        // here is like init block of first constructor
        familiyyy = family
    }

    fun hello() {
        familiyyy.length
    }
}

```




Setter & Getter
---

```kotlin
 val age: Int
        get() = Calendar.getInstance().get(Calendar.YEAR) - yearOfBirth

    var socialSecurityNumber: String = ""
        set(value) {
            if (!value.startsWith("SN")) {
                throw IllegalArgumentException("security number must start with SN")
            }
            //assigning the field value to it
            field = value
        }
```


visibility modifiers
---

default visiblity in kotlin is public.

we have 4 visibility modifiers in kotlin:

	public - Default and anywhere accessible

Top level declarations:
	private - available inside file that containing declarations
	internal - anywhere in the same module(maven,gradle,...)

Classes:
	private - only available to class members
	protected - same as private and subclasses
	internal - Any client inside the module




if we declare a class as data class, kotlin provide toString,hashCode,.... automatically.





enum class
---

```kotlin
enum class Priority {
    Minor,
    Normal,
    Major,
    Critical
}

//use it
   val priority = Priority.Critical
    println(priority)
```


or use with input arg

```kotlin

enum class Priority(val value: Int) {
    Minor(0),
    Normal(1),
    Major(2),
    Critical(3),
}

val priority = Priority.Critical
    println(priority)
    println(priority.value)

    //will prints: Critical \n 3
```

Navigate through enums
```kotlin

    for (priorityInList in Priority.values()) {
        println(priorityInList)
    }

    val p = Priority.valueOf("NORMAL")
    println(p.value)
    println(p.ordinal)
```


override or define custom methods in enum classes
```kotlin
enum class Priority(val value: Int) {
    MINOR(-1) {
        override fun text() {
            println("MINOR PRIORITY")
        }

        override fun toString(): String {
            return "Minor Priority"
        }
    },
    NORMAL(0) {
        override fun text() {
            TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
        }
    },
    MAJOR(1) {
        override fun text() {
            TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
        }
    },
    CRITICAL(2) {
        override fun text() {
            TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
        }
    };
    
    abstract fun text()
}

```


Objects
---

 js doesn't have class concept, but it has objects, and kotlin has it too.

 we use objects to create singleTone objects. actually we create singleTone pattern in kotlin in this way. 

In this example PI is singleTone.

```kotlin
object GlobalObject {
    val PI = 3.14
}


fun main(args: Array<String>) {
    println(GlobalObject.PI)

    val localObject = object {
        var localPI = 3.1415
    }

    localObject.localPI
}
```






casting
---

we cast with 'as' keyword in kotlin,

if we use ? after types or elsewhere, we actually make it type safe and we don't get castException or nullPointerException anymore.

```kotlin

var input: Any = 10

fun main(args: Array<String>) {

    val nullMessage: String?

    val str = input as? String

    println(str?.length)
}
```



Tuples
---

we can use Pair or Triple to return more than one value.

```kotlin
fun getCountryAndPopulation(): Pair<String, Long> {
    return Pair("madrid", 23000000)
}

fun getCountryInfo(): Triple<String, String, Long> {
    return Triple("Madrid", "Euro", 23000000)
}


fun main(args: Array<String>) {
    val population = getCountryAndPopulation()
    println(population.first)
    println(population.second)

    val countryInfo = getCountryInfo()
    println(countryInfo.first)
    println(countryInfo.second)
    println(countryInfo.third)
}
```


decounstructiong
---

A better way to use Pair and others is to use val() instead of first and second ,...

```kotlin
 val (capital, populationn) = getCountryAndPopulation()
 println(capital)
 println(populationn)
```



or 

```kotlin

    val listOfCapitals = listOf(Pair("France", "Madrid"), "Paris" to "France")

    for ((capital2, country) in listOfCapitals) {
        println("country: $country and capital is: $capital")
    }
```


Exceptions
---
checked exceptions removed from kotlin. we just have runTimeExceptions in kotlin.

we can have 'finally' ,'catch' or both blocks. but we need one of them.

like if and when, try/catch blocks also can return value.



Inheritance
---
by default in kotlin all classes are final and we can't inherit from them.
with 'open' keyword we can change a class from final to non-finla.
and also members of calsses are final and we can declare them non-final with open keyword.

```kotlin
open class Person {

    open fun validate() {

    }
}

class Customerr : Person() {

    override fun validate() {

    }
}
``` 


with final keyword we can make some class or member class final and not open.




Abstract classes
---
like java





Declaring Constants
---
we can (and it is better to) group constants with object.

```kotlin
val COPY_RITGH_AUTHOR = "Ali Nasrabadi"

object AUTHOR {
    val COPY_RIGHT = "Ali Nasrabadi"
}


fun main(args: Array<String>) {
    AUTHOR.COPY_RIGHT
    COPY_RITGH_AUTHOR
}

```
 



 Interface
 ---
 one major different between abstract classes and interfaces is the ability to save state. in interfaces we can't do this.

 ```kotlin
import com.sun.org.apache.xpath.internal.operations.Bool

interface CustomerRepository {


    fun getCustomer(id: Int): Customer

    fun store(obj: Customer): Boolean {
        //store customer and return true if successfully inserted
        return true
    }
}


class SQLCustomerRepository : CustomerRepository {

    override fun getCustomer(id: Int): Customer {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

}


interface interface1 {
    fun printA() {
        println("printA from interface1")
    }
}

interface interface2 {
    fun printA() {
        println("printA from interface2")
    }
}

class class1And2 : interface1, interface2 {

    override fun printA() {
        super<interface2>.printA()
    }
}


fun main(args: Array<String>) {
    val c = class1And2()
    c.printA()
}
 ```


 Annotations
 ---
 using annotations in kotlin is similar to java.




 higher-order functions
 ---
 in kotlin we can reference a function by name with '::' like: ::sum or ::minus

 ```kotlin
fun operation(x: Int, y: Int, op: (Int, Int) -> Int): Int {
    return op(x, y)
}

fun sum(x: Int, y: Int) = x + y


fun main(args: Array<String>) {

    println(operation(4, 3, ::sum))
    
}
 ```



 Genric classes
 ---

 we have genrics in kotlin


used like this:

 ```kotlin 
interface Repository<T> {
    fun getById(id: Int): T
    fun getAll(): List<T>
}

class GenericRepository<T> : Repository<T> {
    override fun getById(id: Int): T {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

    override fun getAll(): List<T> {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

}


fun main(args: Array<String>) {
    val repo = GenericRepository<Customer>()

    val customers = repo.getAll()
    val customer = repo.getById(10)
    

}
 ```


 Generic functions
 ---

 use like this when type parameters are different types

 ```kotlin

//Generic functions
interface Repo {
    fun <T> getById(id: Int): T
    fun <R> getAll(): R

}

class MyRepo : Repo {

    override fun <T> getById(id: Int): T {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

    override fun <R> getAll(): R {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }

}

 ```



 Lambda Expresions
 ---

 ```kotlin
 val op: (Int, Int) -> Int = { x, y -> x + y }
    println(operation(3, 2, op))
 ```



it is like language keywords, :D

```kotlin
fun transaction(db: Database, code: () -> Unit) {
    try {
        code()
    } finally {
        db.commit()
    }
}

class Database {
    fun commit() {

    }
}

//usnig it
    val db = Database()
    transaction(db) {
        //do anything code wanna do
    }


```


 Anonymous functions
 ---
with anonymous functions we can have multiple returns without naming the function

```kotlin
    //anonymous functions
    uneryOperation(3, fun(x: Int): Int { return x * x })
```



null safety
---
we can use '?' question mark to null safe a statement that could be null instead of check null with multiples if.

and with '!!' we say to compiler that i khow what i am doing and let me do my job.






clousurs
---

```kotlin

    //closures -  we can use number in the lambda that declared out of lambda expression
    for (number in 1..30) {

        uneryOperation(10, { x ->
            println(number/*number will be change everyTime with new value*/)
            x * number/*number here captured as closure*/
        })
    }
```



Extensions Function
---
we this, we can extend types without having to inherit from them.

like this:

```kotlin
fun String.hello() {
    println("Hello $this")
}

fun String.hello(name: String) {
    println("Hello $name")
}


fun main(args: Array<String>) {
    val string = ""

    string.hello()

    string.hello("ALI")

    "Reza".hello()
}
```



Interoprability with java
---
kotlin is completely Interoprabilble with java. 



checking for null when you interact with java is up to you and IDE do trust in you, nothing else.



we can use jvm annotations in kotlin to support some functionallity in java.

```kotlin
@jvmName("methodNewName")
@jvmField
@jvmOverloads
```




Collections
---
we use listOf to create a list in kotlin.


for using collections in kotlin,it is better to use kotlin helper collections that exists in kotlin.
