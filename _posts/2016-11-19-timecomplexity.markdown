---
layout: post
title:  "Time complexity "
date:   2016-10-19 06:08:02 +0530
---
# Algorithm Efficiency


The complexity of an algorithm is a function describing the efficiency of the algorithm in terms of the amount of data the algorithm must process.

### There are two main complexity measures of the efficiency of an algorithm:

#### Time complexity:
>is a function describing the amount of time an algorithm takes in terms of the amount of input to the algorithm. "Time" can mean the number of memory accesses performed, the number of comparisons between integers, the number of times some inner loop is executed, or some other natural unit related to the amount of real time the algorithm will take.

#### Space complexity:
> is a function describing the amount of memory (space) an algorithm takes in      terms of the amount of input to the algorithm. We often speak of "extra" memory needed, not counting the memory needed to store the input itself. Again, we use natural (but fixed-length) units to measure this. We can use bytes, but it's easier to use, say, number of integers used, number of fixed-sized structures, etc.
Time Complexity:

# O(1):

Time complexity of a function is considered as O(1) if
* it doesn’t contain loop,
* recursion
* call to any other non-constant time function.

A loop or recursion that runs a constant number of times is also considered as O(1).


~~~java
// Here c is a constant
for (int i = 1; i <= c; i++) {
     // some O(1) expressions
}
~~~

# O(n):

Time complexity of a loop is considered as O(n) if the loop variables is incremented / decremented by a constant amount. For example following functions have O(n) time complexity.
~~~java
// Here c is a positive integer constant  
for (int i = 1; i <= n; i += c) {
     // some O(1) expressions
}

for (int i = n; i > 0; i -= c) {
                   // some O(1) expressions
}
~~~
# O(n2):

Time complexity of nested loops is equal to the number of times the innermost statement is executed. For example the following sample loops have O(n2) time complexity
~~~java
for (int i = 1; i <=n; i += c) {
     for (int j = 1; j <=n; j += c) {
                     // some O(1) expressions
      }
}
for (int i = n; i > 0; i += c) {
     for (int j = i+1; j <=n; j += c) {
                     // some O(1) expressions
      }
}
~~~
For example Selection sort and Insertion Sort have O(n2) time complexity.
# O(logn):

Time Complexity of a loop is considered as O(Logn) if the loop variables is divided / multiplied by a constant amount.
~~~java
for (int i = 1; i <=n; i *= c) {
     // some O(1) expressions
}
for (int i = n; i > 0; i /= c) {
    // some O(1) expressions
}
~~~
For example Binary Search  has O(Logn) time complexity.

# How to combine time complexities of consecutive loops?

When there are consecutive loops, we calculate time complexity as sum of time complexities of individual loops.
~~~java
for (int i = 1; i <=m; i += c) {
        // some O(1) expressions
}
for (int i = 1; i <=n; i += c) {
       // some O(1) expressions
}
~~~
**Time complexity:** O(m) + O(n) which is O(m+n)
If m == n, it becomes O(2n) which is O(n).

{% include image.html url="/images/timecomplexity_1.gif" description="Time complexity Graph." %}

# Space Complexity of Recursive Algorithm?

~~~java
long Rsum(int[] a,n)
{
     if(n<=0){
           return 0.0;
     }
     return Rsum(a,n-1)+a[n];
}
~~~
When the function calls itself there are 3 things that are stored in the stack.
>
* The array pointer a,
* The size of the array n and
* The value at the last index a[n].
* This function calls itself till n becomes 0, so there the amount of space required to store these values is n times the space required to store these values once, i.e., nx{sizeof(a)+sizeof(n)+sizeof(a[n])}. Since the value in the braces remain a constant, we say that the space complexity of this is directly proportional to N.

{% include image.html url="/images/timecomplexity_2.gif" description="Complexity Analysis of different Sortings." %}
