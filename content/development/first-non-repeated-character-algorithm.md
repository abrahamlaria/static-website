---
title: "First Non Repeated Character Algorithm"
date: 2018-07-11T00:11:54-07:00
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

Solution to finding the "First Non Repeating Character" problem in C#
<!--more-->
## Problem

Given a string, find and return the first instance on a non-repeating character in it. If the is no such character,
return "_".

**Note:** Write a solution that only iterates over the string once and uses O(1) additional memory.

### Example

Input:

```
"abacabad"
```

Output:

```
'c'
```

Input:

```
"abacabaabacaba"
```

Output:

```
'_'
```

## Algorithm

* Create an Dictionary, O(1) additional memory.
* Iterate over the string.
* If the character at the position i isn't in the Dictionary, add it as a Key and set a default Value of 1.
* If the character at the position i is already in the Dictionary, increment its Value by 1.
* Iterate over the Dictionary.
* Return the Key of the first element with Value = 1.
* Otherwise return '_'.

## Solution

```
using System;
using System.Collections.Generic;

namespace FirstNotRepeatingCharacter
{
    class Program
    {
        public static char FirstNotRepeatingCharacter(string s)
        {
            Dictionary<char, int> dict = new Dictionary<char, int>();

            for (var i = 0; i <= s.Length - 1; i++)
            {
                if (dict.ContainsKey(s[i])) //ContainsKey is aprox. O(1)
                {
                   dict[s[i]]++; //Add 1 to dict.Value
                    
                }
                else
                {
                    dict.Add(s[i], 1);
                }
            }

            foreach (var pair in dict)
            {
                if (pair.Value == 1)
                {
                    return pair.Key;
                }
            }

            return '_';
        }
        
        static void Main(string[] args)
        {
            string s = "abacced";          
            Console.Write(FirstNotRepeatingCharacter(s));
            Console.ReadLine();
        }
    }
}
```

## Another (SLOWER) Solution

This solution replaces the Foreach block on the first solution by using ContainsValue() and then LINQ's First(). it is slower
because it goes twice over the dictionary before returning the character. Also, the use of ContainsValue() is not an improve
ment over Foreach. They are both O(n).

```
using System;
using System.Collections.Generic;
using System.Linq;

namespace FirstNotRepeatingCharacter
{
    class Program
    {
        public static char FirstNotRepeatingCharacter(string s)
        {
            Dictionary<char, int> dict = new Dictionary<char, int>();

            for (var i = 0; i <= s.Length - 1; i++)
            {
                if (dict.ContainsKey(s[i])) //ContainsKey is aprox. O(1)
                {
                   dict[s[i]]++; //Add 1 to dict.Value
                    
                }
                else
                {
                    dict.Add(s[i], 1);
                }
            }

            //Slower solution
            if (dict.ContainsValue(1))
            {
                return dict.First(x => x.Value == 1).Key;
            }

            return '_';
        }
        static void Main(string[] args)
        {
            string s = "abacced";          
            Console.Write(FirstNotRepeatingCharacter(s));
            Console.ReadLine();
        }
    }
}
```

### Constraints

```
The string contains only lowercase English letters.
1 <= string.Length <= 10^5
```
