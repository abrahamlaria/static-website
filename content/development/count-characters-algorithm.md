---
title: "Count Characters Algorithm"
date: 2018-07-10T23:39:09-07:00
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
Solution to counting the number of characters in a given string that are at the same position on the English alphabet. C#
<!--more-->
## Problem

Given a string count he number of characters that are at the same position on the English alphabet.

Check the complete project on my [Github](https://github.com/abrahamlaria/count-characters)

### Example

Input:

```
"ABCde"
```

Output:

```
3
```

## Solution

```csharp
namespace CountCharacters
{
    class Program
    {       
        public static int FindCount(string str)
        {
            var result = 0;

            for (var i = 0; i <= 26; i++)
            {
                //Check if the result of sustracting the ASCII value of the letter in the position [i] of the array and the ASCII
                //value of a or A is equal to the value of i. Increment the counter (result) if one of the operations is true.
                
                if (i == (str[i] - 'a') || (i == str[i] - 'A'))
                {
                    result++;
                    
                    //Print to the console the characters and their position in the string.
                    Console.Write("Character: " + str[i] + " at position: " + i + "\n");
                }                                      
            }
            //Return the total number of found characters
            return result;
        }
        static void Main(string[] args)
        {
            const string str = "ABCed";
            Console.Write("Total number of matching characters: " + FindCount(str));
            Console.ReadLine();
        }
    }
}
```

## Solution using XOR operations

```C#
namespace CountCharacters
{
    class Program
    {       
        public static int FindCount(string str)
        {
            var result = 0;

            for (var i = 0; i <= 26; i++)
            {
                //Check if the result of sustracting the ASCII value of the letter in the position [i] of the array and the ASCII
                //value of a or A is equal to 0 when XOR'd with the value of i. Increment the counter (result) if one of the operations is true. 
                
                if ((i ^ str[i] - 'a') == 0 || (i ^ str[i] - 'A') == 0)
                {
                    result++;
                    
                    //Print to the console the characters and their position in the string.
                    Console.Write("Character: " + str[i] + " at position: " + i + "\n");
                }                                      
            }
            //Return the total number of found characters
            return result;
        }
        static void Main(string[] args)
        {
            const string str = "ABCed";
            Console.Write("Total number of matching characters: " + FindCount(str));
            Console.ReadLine();
        }
    }
}
```
### XOR operations:

```
0 ^ 0 = 0
0 ^ 1 = 1
1 ^ 0 = 1
1 ^ 1 = 1
```
### Other XOR rules:

```
a ^ a = 0
0 ^ a = a
```

