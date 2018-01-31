

<p align="center"><img width="300" height="300" margin="auto" src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/74/Kotlin-logo.svg/2000px-Kotlin-logo.svg.png" /></p>

# Awesome-Kotlin-Snippets [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)


[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity)


A curated list of awesome Kotlin snippets for beginners and advanced developers who want to enhance their productivity & skills with this powerful language.
 
----------

#### Equivalent of Java's main function
```kotlin
object Main {
    @JvmStatic
    fun main(args: Array<String>) {
        // Your code
    }
}
```
----------
#### String interpolation
```kotlin
val dummyVal = 56
val dummyUser = User(name="Foo") 

// Variable interpolation
print("The value of dummyVal is $dummyVal")

// Function interpolation
print("dummyVal * 2 => ${dummyVal*2}")

// Object member interpolation
print("The name of dummyUser is ${dummyUser.name}")
```

----------
#### Execute block of code if not null
```kotlin
val alfred = User(name="Alfred")

alfred?.let {
	// Alfred is not null in this block of code
	// You can access Alfred instance with 'it' keyword
	print("My name is ${it.name}")
}

// Output : My name is Alfred

```
----------
#### Call object function if not null
```kotlin
val alfred = User(name="Alfred")
var batman: User? = null

alfred?.sayHello() // Produces "Hello ! I'm Alfred"
batman?.sayHello() // Nothing happens, no error, nothing.
```
----------
#### Get variable's value or other if the variable is null
```kotlin
 val x = null
 val y = x ?: 3 
 
 // y = 3 because x is null
```
----------
#### Sort hashmap by value
```kotlin
val weights = hashMapOf("Foo" to 68, "Bar" to 30, "Baz" to 10)

// Ascending order
val sortedWeightsAsc = weights.toList().sortedBy { (key,value) -> value }.toMap()

// Descending order
val sortedWeightsDesc = weights.toList().sortedByDescending { (key,value) -> value }.toMap()
```


----------
#### Equivalent of switch case
```kotlin
val choice = "ok"

when (choice) {
   "red" -> {
                //Block of code between curly braces
            }
   "blue" -> print("Blue !!!") // Single instruction
    else -> print("Wut ?") // Default 
}

// Output : Wut ?
```
----------

#### Human-readable object members modification
```kotlin
val toto = User(name="Toto", age=36, dateOfBirth="05-23-1998")

toto.apply {
	name="Foo"
	age=41
	dateOfBirth="01-01-2018"
}

// Now, the members of toto are changed
```
----------
#### Check if element is in list
```kotlin
val numbers = listOf(1,30,45,73,2,19)

if( 1 in numbers ) {
	// Code
}
```
----------
#### Remove elements of a list based on certain conditions
```kotlin
val animals = listOf("black tiger", "white tiger", "red tiger", "golden tiger", "fish", "lion", "cat", "dog")
var tigers: List<String> = emptyList()

// Contains style
tigers = animals.filter { it.contains("tiger") }

// Kotlin style
tigers = animals.filter { "tiger" in it }

// Kotlin parameterized style
tigers = animals.filter { animal -> "tiger" in animal }

print(tigers)

// Output : [black tiger, white tiger, red tiger, golden tiger]
```
----------
#### Apply function to all elements of a list
```kotlin
val numbers = listOf(1,2,3,4,5)
val doubles = numbers.map { it*2 }

print(doubles)

// Output : [2,4,6,8,10]
```
----------
#### Check that at least one element of a list verifies conditions
```kotlin
val numbers = listOf(1,2,3,4,5)

if(numbers.any { it > 4 } )
	print("At least one element > 4")

// Output : At least one element > 4
```
----------
#### Retrieve the first element of a list matching conditions
```kotlin
val animals = listOf("black tiger", "white tiger", "red tiger", "golden tiger", "fish", "lion", "cat", "dog")
val firstTiger = animals.first { it.contains("tiger") }

// You can replace firt with firstOrNull, self-explanatory
print(firstTiger)

// Output : black tiger
```
----------
#### Variable conditional assignation
```kotlin
val a = 5

val x = when(a) {
	1 -> "a is equal to 1"
	3 -> "wut ?"
	else -> "a is a big int"
}

// x = "a is a big int", because of a = 5 
```
----------
#### Human-readable for loops
```kotlin
for (i in 1..5)
	print(i) // Produces 12345

for (i in 1 until 5)
	print(i) // Produces 1234

for (i in 5 downTo 1)
	print(i) // Produces 54321

for (i in 1..5 step 2)
	print(i) // Produces 135

for (i in listOf("foo","bar","baz"))
	print(i) // Produces foobarbaz

for ( (ingredient,quantity) in hashMapOf("apple" to 3, "steak" to 8, "milk" to 3) )
           print("There are $quantity $ingredient(s) in this cart\n")

/* Last output : 
		There are 8 steak(s) in this cart
		There are 3 milk(s) in this cart
		There are 3 apple(s) in this cart
*/

```
----------
#### Extend an existing object with your own function
```kotlin
fun Int.power(b: Int): Int { 
    var tmpInt = this
    
    if (b == 0) 
        return 1

    for (i in 1 until b)
        tmpInt *= this

    return tmpInt
}

print(2.power(10)) // Produces 1024
```
----------
#### Use infix notation to have a more readable and beautiful code
```kotlin
infix fun Int.power(b: Int): Int { 
    var tmpInt = this
    
    if (b == 0) 
        return 1

    for (i in 1 until b)
        tmpInt *= this

    return tmpInt
}

print(2 power 10) // Produces 1024
```
----------
#### Higher-order functions aka functions passed as parameters
```kotlin
fun logCallTo(function: () -> Unit) { // () -> Unit means the function given as parameter should not have any parameter, and should return nothing 
   print("Log: ----------- The function is about to start ----------\n")
   function()
   print("Log: ----------- The function ended correctly ------------\n")
}

fun wut() = print("Hello there ! I'm wut function\n")

logCallTo { wut() } 

/* Output :
			Log: ----------- The function is about to start ----------
			Hello there ! I'm wut function
			Log: ----------- The function ended correctly ------------
*/
```
----------
#### Design pattern Strategy thanks to higher-order functions

```kotlin
abstract class TextFormattingStrategy {
    abstract fun format(text: String): String
}


class UnderlineStrategy : TextFormattingStrategy() {
    override fun format(text: String): String {
        return "<u>$text</u>"
    }
}

class BoldStrategy : TextFormattingStrategy() {
    override fun format(text: String): String {
        return "<strong>$text</strong>"
    }
}

class ItalicStrategy : TextFormattingStrategy() {
	// You can use this syntax too
    override fun format(text: String): String = "<i>$text</i>" 
}

fun format(text: String, strategy: TextFormattingStrategy): String {
    return strategy.format(text)
}

val text = "Awesome text !"

print(format(text, UnderlineStrategy())) // Produces <u>Awesome text !</u>
print(format(text, BoldStrategy()))      // Produces <strong>Awesome text !</strong>
print(format(text, ItalicStrategy()))    // Produces <i>Awesome text !</i>
```
----------
#### Measure time elapsed  during function execution 
```kotlin
fun longTreatment() {
	   for (i in 0..10000000000) {
	       // Nothing, just keep running
	   }
}

// This function is part of the Kotlin Standard Library
print(measureTimeMillis { longTreatment() }) // Produces 4323 ms
```
----------
#### Declare a Matrix / 2D Array
```kotlin
inline fun <reified T> matrix(height: Int, width: Int, initialize: () -> T) = Array(height) { Array(width) { initialize() } }

val board = matrix(5, 5) { 0 }

board.forEach { row ->
    row.forEach { column ->
        print("$column ")
    }
    print("|\n")
}

/* Output : 
		0 0 0 0 0 |
		0 0 0 0 0 |
		0 0 0 0 0 |
		0 0 0 0 0 |
		0 0 0 0 0 |    
*/        
```


----------
#### Declare a class in charge of holding data solely
```kotlin
data class User(val name: String, val age: Int)

// Notice that in Kotlin the 'new' keyword doesn't exist
val toto = User("Toto", 18)

// You can initialize objects with named arguments
val foo = User(name = "Foo", age = 19)

// You can access members of those objects directly
print("Hello, I'm ${toto.name}\n")
print("I'm his friend ! ${foo.name} - ${foo.age}yo !")

/* Output :
			Hello, I'm Toto
			I'm his friend ! Foo - 19yo !
*/
```
----------
#### Declare a singleton
```kotlin
data class User(val name: String, val age: Int)

object UserFactory { // Practice design patterns while learning Kotlin <3
	val userList: ArrayList<User> = ArrayList()

	fun createUser(name: String, age: Int): User {
	    val createdUser = User(name, age)
	    userList.add(createdUser)
	    return createdUser
	}
}

// Notice that UserFactory is called without having been instantiated before with something like 'val uf = UserFactory()'
val foo = UserFactory.createUser("Foo",18)
``` 
----------
#### Operator overloading
See full reference at : [Kotlin overloading operators reference](https://kotlinlang.org/docs/reference/operator-overloading.html) :thumbsup:
```kotlin
operator fun Int.not(): Int {  // operator overloaded : !
    var tmpInt = 1
    for (i in 1..this) // Basic factorial implementation
        tmpInt *= i
    return tmpInt
}

print(!5) // Produces 120
```
----------
#### Using an object as a context
```kotlin
val toto = User(name="Toto", age=18)

with(toto) {
	print(name) 	// First syntax, omit 'toto' and omit 'this'
	print(this.age) // Yay ! Second syntax
}
```
----------
#### Cool syntactic sugars
```kotlin
/*************************************************************/
val cart = hashMapOf("apple" to 3, "steak" to 8, "milk" to 3)

// You can use the '_' wildcard for parameters you don't use
val vegetables = cart.filter { (key,_) -> "steak" !in key }

/*************************************************************/
fun logExecution(a: Int, b: String, f: () -> Unit) {
	// Code
}

// If a function is passed as the last parameter of a higher-order function, you can write it like this
logExecution(3,"dummy string") { print("Hello !" } 

// Instead of (inside parenthesis)
logExecution(3, "dummy string", { print("Hello !") } )

/*************************************************************/
Incoming <3
```

## Contributing

Feel free to open issues and pull requests so that this repository becomes even more useful ! 

Kotlin is a rich and powerful language, you're encouraged to share your valuable knowledge :heart::purple_heart::yellow_heart: 

**It will help a lot of newcomers and experienced developers too**

Take a look at [CONTRIBUTE.md](CONTRIBUTE.md) so that your PRs are easily added  and respect basic guidelines so that everything is cool and easy to re-use.

## Disclaimer

This repository does not aim to replace the original Kotlin documentation at all ! It has been created only to provide a centralized place for common useful snippets we're all searching for :unicorn: :sparkles:

The official Kotlin documentation is very nice, you should give it a look : 
<a href="https://kotlinlang.org/docs/reference/">https://kotlinlang.org/docs/reference/</a>
