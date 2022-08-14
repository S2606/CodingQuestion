### The question

You are given a 0-indexed string pattern of length n consisting of the characters 'I' meaning increasing and 'D' meaning decreasing.

A 0-indexed string num of length n + 1 is created using the following conditions:

    num consists of the digits '1' to '9', where each digit is used at most once.
    If pattern[i] == 'I', then num[i] < num[i + 1].
    If pattern[i] == 'D', then num[i] > num[i + 1].

Return the lexicographically smallest possible string num that meets the conditions.
 

Example 1:
```
Input: pattern = "IIIDIDDD"
Output: "123549876"
Explanation:
At indices 0, 1, 2, and 4 we must have that num[i] < num[i+1].
At indices 3, 5, 6, and 7 we must have that num[i] > num[i+1].
Some possible values of num are "245639871", "135749862", and "123849765".
It can be proven that "123549876" is the smallest possible num that meets the conditions.
Note that "123414321" is not possible because the digit '1' is used more than once.
```

Approach:- 

```
1 2 3 4 5 6 7 8 9
D D I D D I D D

The logic is quite simple, while char is 'D', keep adding the char (auto-increment number converted to char). Once you find an 'I', simply reverse the stack and append it to the response. How exactly?

Lets take the example above, and try to maintain a stack for dry-run purposes

1
stk [1]
char 'D'
res []

1 2
stk [1, 2]
char 'D'
res []

1 2 3
stk [1, 2, 3]
char 'I' time to reverse and fill it in res
res [3, 2, 1]

1 2 3 4
stk [4]
char 'D'
res [3, 2, 1]

1 2 3 4 5
stk [4, 5]
char 'D'
res [3, 2, 1]

1 2 3 4 5 6
stk [4, 5, 6]
char 'I' time to reverse and fill it in res
res [3, 2, 1, 6, 5, 4]

1 2 3 4 5 6 7
stk [7]
char 'D'
res [3, 2, 1, 6, 5, 4]

1 2 3 4 5 6 7 8
stk [7, 8]
char 'D' since we have reached end of string, time to reverse and fill it in res
res [3, 2, 1, 6, 5, 4, 8, 7]
```

Lets code:-
```
public String smallestNumber(String pattern) {
   StringBuilder res = new StringBuilder(), stack = new StringBuilder();
   for(int i=0;i<=pattern.length();i++){
       stack.append((char)('1'+i));
       if(i==pattern.length() || pattern.charAt(i)=='I'){
           res.append(stack.reverse());
           stack = new StringBuilder();
       }
   }

   return res.toString();
}
```

- Time complexity - O(n)
- Space complexity - O(n)
