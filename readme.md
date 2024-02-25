# MAD - Exercise 01

## Tasks

- Watch the Kotlin Crashcourse Video in Moodle or complete the tutorials **[Introduction to programming in Kotlin](https://developer.android.com/courses/pathways/android-basics-compose-unit-1-pathway-1)** and **[Kotlin fundamentals](https://developer.android.com/courses/pathways/android-basics-compose-unit-2-pathway-1)**.
- Answer the questions inside this Readme.md file and push it to your repository.
- Submit your coding solution of the Number Guessing Game inside the repository.
- Submit the link to your repository in Moodle.

## Questions

### Describe how Kotlin handles null safety. What are nullable types and non-null types in Kotlin? (0,5 points)

<span style="color:blue">Provide your answer here! </span>

In Kotlin there are both nullable and non-null types. Null safety helps prevent null pointer exceptions. The types are non-nullable by default, which means when making a variable the usual way, it will give an error.

```kotlin
val myString: String = null // This will give an error.
```

We need to declare the string as nullable. We achieve that by adding a "?" at the end of the data type.

```kotlin
val myString: String? = null // This will not give an error.
```

We can also use safe calls to make sure a variable we are accessing is not null.

```kotlin
val myString: String? = "Stefan"
println(myString?.uppercase()) // If myString was not null, it would run the code further (in this case .uppercase()), if not it wouldn't run the rest of it.
```

Assertion calls are another way that can be used, but we should rarely use this, only if we are CERTAIN that the variable we are accessing is not null.

```kotlin
val myString: String? = "Stefan"
println(myString!!.uppercase()) // This would run the code, regardless if myString was null or not, which can lead to null-pointer exceptions
```

### What are lambda expressions and higher order functions in Kotlin? Why would you store a function inside a variable? (0,5 points)

<span style="color:blue">Provide your answer here!</span>

Lambda expressions allow us to store functions inside a variable. This can make it easier to write more resuable and modular code. Higher order functions are functions that can take another function as a parameter.
I will elaborate this a bit more with some code.

```kotlin
val printMessage: (String) -> Unit = {println("This is your message: $it")} // This is a lambda expression, that takes a string as a parameter and doesn't return anything (Unit == void in Java). We can access the parameter with "it" when there only is one parameter.

fun printCustomMessage(message: String, printMessage: (String) -> Unit) { //This declares a function that takes a string and a function as a parameter (higher order function) and calls that method that is being passed with the parameter.
	printMessage(message)
}

printCustomMessage("My message", printMessage) // We can call this function now by giving it a string and the "printMessage" lambda we have declared before. Output: "This is your message: My message"
```

### Provide a solution for the following number guessing game inside `App.kt`. (3 points)

## Number Guessing Game in Kotlin

The game is a simple number guessing game. The task is to generate a random, max 9-digit, number. The number must **not contain repeating digits**. Valid digits are 1-9.
Ask the user to guess the max 9-digit number. The game is finished when the user guesses the correct digits in the correct order.
In each round, the user gets feedback about the number of correct digits and the number of correct digits in the correct position.
The output should be in the format "n:m", where "n" is the number of digits guessed correctly regardless of their position,
and "m" is the number of digits guessed correctly at their correct position. Here are some examples:

This example shows the game flow with 4-digits to guess (the default argument)

Generated number: 8576

- User input: 1234, Output: 0:0
- User input: 5678, Output: 4:1
- User input: 5555, Output: 1:1
- User input: 3586, Output: 3:2
- User input: 8576, Output: 4:4 -> user wins

Take a look into the provided code structure in `src/main/kotlin/App.kt`. Implement the following methods (lambda expressions):

- _playNumberGame(digitsToGuess: Int = 4)_ (1 point): The main game loop that handles user input and game state. Make use of _generateRandomNonRepeatingNumber_ and _checkUserInputAgainstGeneratedNumber_ here. This function also utilizes a default argument
- _generateRandomNonRepeatingNumber_ (1 point): A lambda expression that generates a random number with non-repeating digits of a specified length.
- _checkUserInputAgainstGeneratedNumber_ (1 point): A lambda expression that compares the user's input against the generated number and provides feedback.

`CompareResult.kt` This class is a data structure which helps with bundling the result of the comparison of the user input and the generated number. Look at the toSting() and use it in your output.

Run the project with `./gradlew run` and test your implementation with the provided tests in `src/test/kotlin/AppTest.kt` with `./gradlew test`.

# Project Structure

The project is structured into two main Kotlin files:

**App.kt**: Contains the main game logic and functions.

**AppTest.kt**: Contains unit tests for the various functions in App.kt.
