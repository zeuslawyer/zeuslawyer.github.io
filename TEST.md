# TEST PAGE

__DOES THIS WORK?__



WHY THE HECK ISNT THIS PUBLISHING??

# Big O
“Big O” notation is an abstracted representation of concepts of complexity, specifically the following two types of complexity in computing software:

1. Time Complexity - the amount of time a given algorithm takes to spit put the answer ( a function of the number of operations it needs to carry out, and whether that time is correlated with the size of data to be processed; and
2. Space Complexity - how much memory space does the *algorithm* (not the inputs it processes) take up?   This is the ***auxiliary space complexity***.

In both cases the complexity is expressed as a function of the number of inputs that need to be algorithmically processed, and that number is referred to as `n`.

**Time Complexity**
If the operations in an algorithm take a constant time regardless of how many data inputs it needs to process, then we need a way to express that constant time factor. This is : `O(1)`.
If the time increases in proportion (linear or exponential) to the number of inputs that need processing,  then we express it as `O(n)`, where `n` is the number of items that are processed.  The higher `n` is, the longer the algorithm will take.  This is an analysis of the ***runtime*** complexity of an algorithm.

**Examples of Time Complexity**

    
    //METHOD 1 using Loop
    function sumTill(n) {
      let res = 0;
      for (let i=0; i<=n; i++) {
        res +=i
      }
      return res
    }
    
    //METHOD 2 no loop
    function sumTillWithoutLoop(n){
      return n * (n+1)/2;
    }
    

These are two implementations of an algorithm that sums all the numbers from 0 up till, and including, the number passed into the function.

In **Method 1**, we use a for loop.   For each pass over the loop, there are operations (denoted by the <, +, =, ++ signs etc). Therefore, the number of loops is equal to `n` that is passed in as the argument, which the number if iterations of the loop scales in proportion to the upper bounds of the argument.   This is `O(n)` - a linear increase in time complexity, proportionate to the value of `n`.

In **Method 2**, we use a formula to compute the sum of all the numbers up till and including `n`.  But there is no loop, and the number of operations are equal to 3, regardless of what value `n` has.  The operations do ***not*** increase in proportion to the size of the argument.  This is `O(1)` - a constant time complexity regardless of the value of `n`.

Big O is not meant to be precise, but an approximate abstraction of the concept of complexity. Technically, some algorithms may have complexity that looks like this :  `O(n^3 + n^2)`.

But, the purpose of Big O is to show the worst case complexity, and this can be approximated by conveying that  `O(n^3 + n^2)` is, for practical purposes, effectively  `O(n^3)` because the addition of `n^2`  is subsumed within the complexity implied by `n^3`.  Similarly, we can strip away multiples of `n` that are constant values:  for example `O(4n)` can be expressed as `O(n)`.

**Exponential complexity**
Sometimes, the complexity is exponential.  For example, in nested loops like this one:

        function subtotals(array) {
          var subtotalArray = Array(array.length);
          for (var i = 0; i < array.length; i++) {
            var subtotal = 0;
            for (var j = 0; j <= i; j++) {
              subtotal += array[j];
            }
            subtotalArray[i] = subtotal;
          }
          return subtotalArray;
        }


**Auxiliary Space Complexity**
Most primitiva data types (`bools, integers, numbers, undefined, null`) are constant space complexity.  But not `strings` which are `O(n)` complexity, where `n` is the string’s length, as the more characters (including whitespaces) a string contains, the more space it takes up. Similar to strings, JavaScript reference types (Arrays and Objects) are `O(n)` complexity, where `n` is the array length and the number of keys, respectively.


**Useful tool**
https://rithmschool.github.io/function-timer-demo/
this tool visualises a few basic algoirthms to show you how the browser deals with complexity of those algorithms.


**Great (but unrelated) Song**

https://www.youtube.com/watch?v=XJTTp-ipE8M&


[https://youtu.be/XJTTp-ipE8M](https://youtu.be/XJTTp-ipE8M)


