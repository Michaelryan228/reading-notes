After a long time learning and working with object-oriented programming, I took a step back to think about system complexity.
“Complexity is anything that makes software hard to understand or to modify." — John Outerhout
Doing some research, I found functional programming concepts like immutability and pure function. Those concepts are big advantages to build side-effect-free functions, so it is easier to maintain systems — with some other benefits.
In this post, I will tell you more about functional programming, and some important concepts, with a lot of code examples. In Javascript!
What is functional programming?
Functional programming is a programming paradigm — a style of building the structure and elements of computer programs — that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data — Wikipedia
Pure functions
The first fundamental concept we learn when we want to understand functional programming is pure functions. But what does that really mean? What makes a function pure?
So how do we know if a function is pure or not? Here is a very strict definition of purity:
It returns the same result if given the same arguments (it is also referred as deterministic)
It does not cause any observable side effects
It returns the same result if given the same arguments
Imagine we want to implement a function that calculates the area of a circle. An impure function would receive radius as the parameter, and then calculate radius * radius * PI:

Why is this an impure function? Simply because it uses a global object that was not passed as a parameter to the function.
Now imagine some mathematicians argue that the PI value is actually 42and change the value of the global object.
Our impure function will now result in 10 * 10 * 42 = 4200. For the same parameter (radius = 10), we have a different result. Let's fix it!

TA-DA 🎉! Now we’ll always pass thePI value as a parameter to the function. So now we are just accessing parameters passed to the function. No external object.
For the parameters radius = 10 & PI = 3.14, we will always have the same the result: 314.0
For the parameters radius = 10 & PI = 42, we will always have the same the result: 4200
Reading Files
If our function reads external files, it’s not a pure function — the file’s contents can change.

Random number generation
Any function that relies on a random number generator cannot be pure.

It does not cause any observable side effects
Examples of observable side effects include modifying a global object or a parameter passed by reference.
Now we want to implement a function to receive an integer value and return the value increased by 1.

We have the counter value. Our impure function receives that value and re-assigns the counter with the value increased by 1.
Observation: mutability is discouraged in functional programming.
We are modifying the global object. But how would we make it pure? Just return the value increased by 1. Simple as that.

See that our pure function increaseCounter returns 2, but the counter value is still the same. The function returns the incremented value without altering the value of the variable.
If we follow these two simple rules, it gets easier to understand our programs. Now every function is isolated and unable to impact other parts of our system.
Pure functions are stable, consistent, and predictable. Given the same parameters, pure functions will always return the same result. We don’t need to think of situations when the same parameter has different results — because it will never happen.
Pure functions benefits
The code’s definitely easier to test. We don’t need to mock anything. So we can unit test pure functions with different contexts:
Given a parameter A → expect the function to return value B
Given a parameter C → expect the function to return value D
A simple example would be a function to receive a collection of numbers and expect it to increment each element of this collection.

We receive the numbers array, use map incrementing each number, and return a new list of incremented numbers.

For the input [1, 2, 3, 4, 5], the expected output would be [2, 3, 4, 5, 6].
Immutability
Unchanging over time or unable to be changed.

“Change neon light signage” by Ross Findon on Unsplash
When data is immutable, its state cannot change after it’s created. If you want to change an immutable object, you can’t. Instead, you create a new object with the new value.
In Javascript we commonly use the for loop. This next for statement has some mutable variables.

For each iteration, we are changing the i and the sumOfValue state. But how do we handle mutability in iteration? Recursion!

So here we have the sum function that receives a vector of numerical values. The function calls itself until we get the list empty (our recursion base case). For each "iteration" we will add the value to the total accumulator.
With recursion, we keep our variables immutable. The list and the accumulator variables are not changed. It keeps the same value.
Observation: Yes! We can use reduce to implement this function. We will cover this in the Higher Order Functions topic.
It is also very common to build up the final state of an object. Imagine we have a string, and we want to transform this string into a url slug.
In OOP in Ruby, we would create a class, let’s say, UrlSlugify. And this class will have a slugify! method to transform the string input into a url slug.

Beautiful! It’s implemented! Here we have imperative programming saying exactly what we want to do in each slugify process — first lower case, then remove useless white spaces and, finally, replace remaining white spaces with hyphens.