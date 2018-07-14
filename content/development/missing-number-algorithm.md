---
title: "Missing Number Algorithm"
date: 2018-07-11T00:06:14-07:00
draft: false
image: "uploads/Algorithms.jpg"
type: "post"
tags: [
    "algorithms",
]
categories: [
    "development",
]
---
Solution to finding the missing number problem in C#
<!--more-->
## Problem

Given a list of n-1 integers in the range of 1 to n. There are no duplicates in the list. One of the integers is missing in the list. Find it!

### Example

Input:

```
[1, 2, 4, 6, 3, 7, 8]
```

Output:

```
5
```

### Given that

```
1 + 2 + 3 + ... + n = n*(n + 1)/2
```
It can be proved by mathematical induction.

## Solution

```
namespace MissingNumber
{
    class Program
    {
        public static int FindMissing(int[] array, int n)
        {
            var total = n*(n+1)/2;

            for (int i = 0; i < n-1; i++)
            {
                total -= array[i];
            }

            return total;
        }
        static void Main(string[] args)
        {
            int[] array = { 1, 2, 4, 5, 6 };
            Console.Write(FindMissing(array, 5));
            Console.ReadLine();
        }
    }
}

```

**Note:** As stated above n*(n+1)/2 is the same as adding numbers from 1 to n. Knowing that let's solve the problem for n = 5.

Input:

```
[1, 2, 4, 5, 6]
```
Expected Output:

```
3
```
n = 5

```
n*(n+1)/2 = 5*(5+1)/2 = 5*(6)/2 = 30/2 = 15
1 + 2 + 3 + 4 + 5 = 15
15 = 15
```
The algorithm continues by sustracting 15 and the first number in the array and using the result to do the same with the next number in the array up to n - 1.

```
n - 1 = 4 // We are going to iterate from 0 to 4 not including the 4.
array[0] = 1 | 15 - 1 = 14
array[1] = 2 | 14 - 2 = 12
array[2] = 4 | 12 - 4 = 8
array[3] = 5 | 12 - 5 = 3 // This is the missing number!
```
And that solves the problem. Hope that helps!
