# LoopAndLabel

Kotlin practice exercises on loops (`for`, `while`, `do-while`), loop control (`break`, `continue`) and labels.

## Concepts covered

- `for`: used when we know the sequence to iterate over.
  - `1..5` includes 5, `1 until 5` excludes 5.
  - `5 downTo 1` counts down, `1..10 step 2` skips values.
  - We can loop over a list or over a String (one character at a time).
- `while`: checks the condition first and runs as long as it is true. The body may never run.
- `do-while`: runs the body first, then checks the condition. The body always runs at least once.
- `break`: exits the loop immediately.
- `continue`: skips the rest of the current iteration and moves to the next one.
- Labels: in nested loops, `break` and `continue` only affect the inner loop. A label (`outer@`) lets us target the outer loop with `break@outer` or `continue@outer`.

## Exercise 1: Multiplication table

Display the multiplication table of a number entered by the user, then the odd multipliers using `step`, then a countdown using `downTo`.

```kotlin
println("Enter a number to get its multiplication table")
val numberInput = readln().toInt()

println("-----")

for (i in 1..10) {
    val calculatedNumber = numberInput * i
    println("$numberInput * $i = $calculatedNumber")
}

for (i in 1..10 step 2) {
    println("Odd number: $i")
}

println("-----")

for (count in numberInput downTo 1) {
    println("Countdown: $count")
}
```

## Exercise 2: ATM

The user has 3 attempts to enter the correct PIN. After 3 wrong attempts, the card is blocked.

```kotlin
val nip = "1234"
var trials = 0
var password: String

do {
    println("Enter your nip to log in: ")
    password = readln()
    trials++
    if (password == nip) {
        println("Access authorized")
    } else {
        println("Incorrect NIP")
    }
} while (trials < 3 && password != nip)

if (password != nip) {
    println("Card blocked")
}
```

## Exercise 3: Letter search

Search for a letter entered by the user in a list of words, using nested loops and a label.

```kotlin
println("Enter a letter: ")
val letter = readln().first()

val words = listOf("kotlin", "android", "compose", "java")

outer@ for (word in words) {
    for (c in word) {
        if (c == letter) {
            println("Found letter: $letter in $word")
            continue@outer
        }
    }
    println("Absent from $word")
}
```

## What I learned

- One loop iteration should match one action. Reading the input twice in the same iteration breaks the logic.
- A variable declared inside a `do-while` cannot be used after the loop. It must be declared before the `do`.
- A nested loop runs completely for each iteration of the outer loop.
- A simple `break` only exits the inner loop, so the code after it still runs. `continue@outer` jumps straight to the next iteration of the outer loop and skips that code.
- Values should come from variables, not be written by hand (hardcoded) in the messages.