---
title: "First Duplicate Algorithm"
date: 2018-07-11T00:17:40-07:00
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
# First Duplicate
Solution to the "First Duplicate" problem in C#.
<!--more-->
## Problem

Given an array that contains only numbers in the range 1 to array.Length, find the first duplicate number for which the second occurrence has the minimal index. If there is no such number, return -1.

**Note:** Write a solution with O(n) time complexity and O(1) additional space complexity.

Check the complete project on my [Github](https://github.com/abrahamlaria/first-duplicate)

### Example

Input:

```
[2, 3, 3, 1, 5, 2]
```

Output:

```
3
```
There are 2 duplicates: 2 and 3. the second occurrence of 3 has smaller index (position 2 of the array) than the second occurrence
of 2 (position 5 of the array). Hence the first duplicate is 3.

Input:

```
[2, 4, 3, 5, 1]
```

Output:

```
- 1
```
There is not duplicated numbers in the array.

## Solution

```csharp
using System;
using System.Collections.Generic;

namespace FirstDuplicate
{
    class Program
    {
        public static int FirstDuplicate(int[] a)
        {

            HashSet<int> set = new HashSet<int>();

            for(var i = 0; i <= a.Length - 1; i++)
            {
                if (set.Contains(a[i]))
                {
                    return a[i];
                }

                set.Add(a[i]);
            }

            return -1;
        }
        static void Main(string[] args)
        {
            int[] arr = {2, 3, 3, 1, 5, 2};
            Console.Write(FirstDuplicate(arr));
            Console.ReadLine();

        }
    }
}
```

### Constraints

```
1 <= array.Length <= 10^5
1 <= array[i] <= a.length
```

