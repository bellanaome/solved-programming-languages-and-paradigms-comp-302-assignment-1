Download Link: https://assignmentchef.com/product/solved-programming-languages-and-paradigms-comp-302-assignment-1
<br>
This assignment focuses on basic use of Scala and functional programming. Your code must run without error or modification using Scala 2.12.

Note that you must follow the given naming, input, and output requirements precisely. All code should be well-commented, in a professional style, with appropriate variables names, indenting (uses spaces and avoid tabs), etc. The onus is on you to ensure your code is clear and readable. Marks will be very generously deducted for bad style, lack of clarity, or failing to follow the required instructions.

Your code should endeavour to follow a pure functional programming style. In particular, and unless specifically stated otherwise, all data types must be <em>immutable</em>, and <em>data may not be modified once assigned or bound</em>. Note that this means you may not use var declarations, while or do-loops, ArrayBuffers or other mutable structures, nor may you reassign Array element values after creation.

<ol>

 <li>Euler showed that the infinite series converges to. 4</li>

</ol>

<table width="654">

 <tbody>

  <tr>

   <td width="647">Use this property to approximate the value of <em>π</em>. Define a function euler which receives an Int argument and returns an approximation of <em>π </em>using the first <em>k </em>terms of the series, as a Double result.Note that this function does not converge very fast, and you may need a fairly large value of <em>k </em>to get many digits of <em>π </em>correct. If you are using a command-line scala invocation you can increase the stack size by passing a stack size option to the underlying JVM, like “scala -J-Xss4M yourprogram.scala”.</td>

   <td width="7"> </td>

  </tr>

  <tr>

   <td width="647">2. Lists can be understood as recursive structures, as constructed by Scala’s right-associative “::” operator. For example, the list “1::2::3::4::Nil” is a simplified view of how it is actually constructed, as “1::(2::(3::(4::Nil)))”.Define a function show which accepts a List of Any type, and returns a String representation that reflects its actual construction. For example,show(1::2::3::4::Nil) // returns: 1::(2::(3::(4::Nil))) show(1::Nil) // returns: 1::Nil show(Nil) // returns: Nil</td>

   <td width="7">4</td>

  </tr>

  <tr>

   <td width="647">3. A Fibonacci function is easy to define recursively, but done naively it is inefficient, re-computing the same Fibonacci value many times as it recursively descends down both recursive calls. For example, given a definition,</td>

   <td width="7">5</td>

  </tr>

 </tbody>

</table>

def fib(n:Int):Int = { if (n&lt;2) 1 else fib(n-1)+fib(n-2) }

calling fib(5) ends up computing fib(3) twice, fib(2) thrice, and the base case of fib(1) or fib(0) 8 times during the course of its recursive unfolding.

Come up with a more efficient version, fib2 (with the same type signature) that only ever computes a given Fibonacci number once.

Note that you can time your code to observe the difference. For this you can use,

import System.nanoTime def profile[R](code: =&gt; R, t: Long = nanoTime) = (code, nanoTime – t) which executes the given code, returning a pair of values consisting of the result, and the time taken (in nanoseconds). For example, on my systems, executing “profile { fib(33) }” results in

“(5702887,32452005)” (with significant variance in the timing)

Your fib2 version should be at least an order-of-magnitude faster (for non-trivial inputs).

nb: Do not actually include any timing code or executions in your solution, just provide the improved function definition.

<table width="654">

 <tbody>

  <tr>

   <td width="647">4. Lex Luther stole too many cakes. He actually only wants to have stolen exactly 40, but ended up with more, and so has come up with a complicated scheme for returning some of them. Having stolen <em>n </em>cakes, he decided he can return cakes subject to the following, recursively applied conditions:If <em>n </em>is even, he may return <em>n/</em>2 cakes.If <em>n </em>is divisible by 3 or 4, multiple together the last 2 digits of <em>n</em>, and he may return that many cakes. If <em>n </em>is divisible by 5, he can give back exactly 40 cakesThis approach may or may not allow him to reduce the number of cakes he has to 40. Come up with a Scala function, cakes which accepts an Int argument <em>n </em>and returns a Boolean value, true if <em>n </em>cakes can be reduced to 40, and false otherwise.Your function should give a correct answer given any non-negative integer. To help test it, note that:for ( i &lt;- 38 to 100 if (cakes(i)) ) yield ishould return a collection consisting of: 40, 64, 75, 80.Of course other values will be tested too.</td>

   <td width="7">5</td>

  </tr>

  <tr>

   <td width="647">5. Recall (or discover) that a simple polygon is a closed sequence of <em>n &gt; </em>2 non-intersecting, connected straight-line segments. We can represent it as a series of ordered pairs of numbers (coordinates), moving either clockwise or counter-clockwise around the boundary. For example the polygon,</td>

   <td width="7">6</td>

  </tr>

 </tbody>

</table>

can be represented in a text file as <em>n </em>pairs of numbers,

1 24

20 15

18 29

35 17

10 -3

The “Shoelace Formula” is a well known technique for computing the area of any simple polygon. It computes the area from the formula,

Area

Give a scala function that computes the area of a polygon. Your shoelace function should receive the name of file containing coordinates as a String, and return the area as a Double value.

You can assume the coordinate file contains nothing other than the coordinates, although the amount of “whitespace” (spaces, tabs, newlines, carriage-returns) between numbers may vary (but they will be separated by some).

<ol start="6">

 <li>Scala has many ways of doing simple processing from one String into another; making a String upper- 8 case or lower-case is trivial, you can reverse, sort, filter characters, and many other operations. We can chain these operations together fairly easily, but it can turn into a long sequence of syntax.</li>

</ol>

The goal here is to construct a function that can assemble multiple operations together, returning a new function that internally applies several String operations in sequence to its input.

Define a function stringPipeline. It should accept a single argument, a String consisting only of characters in the set {’U’,’T’,’l’,’r’,’s’,’*’}. It returns a function that accepts a String and returns a String.

The input to your stringPipeline function encodes the operations you want to perform.

’U’    convert the string to upper-case

’l’     convert the string to lower-case

’T’ convert the string to title-case (capitalize the first non-space character, and the first character of each word, where words are sequences of characters separated by one or more spaces) ’r’ reverse the string

’s’     sort the characters

’*’     delete all space-characters

For example, an input of “Ts*” means to convert it to title case, sort it, and then delete all spaces.

The returned function encapsulates the multiple operations given by the input string. It can then be applied to a string, performing all the operations requested, in order. For example,

val p = stringPipeline(“Ts*”)

gives a function that will do the 3 operations mentioned above. Thus,

p(” abc def ghi x ! 1″) // result: !1ADGXbcefhi

<h1>What to hand in</h1>

Submit your assignment to <em>MyCourses</em>. Note that clock accuracy varies, and late assignments will not be accepted without a medical note: do not wait until the last minute. Assignments must be submitted on the due date before 6pm.

For each question <em>n</em>, include a file qn.scala with the source code of your answer. Do not define a main.

This assignment is worth 10% of your final grade.                                                                                                                          32