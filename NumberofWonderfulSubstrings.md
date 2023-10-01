## The question

A wonderful string is a string where at most one letter appears an odd number of times.

    For example, "ccjjc" and "abab" are wonderful, but "ab" is not.

Given a string word that consists of the first ten lowercase English letters ('a' through 'j'), return the number of wonderful non-empty substrings in word. If the same substring appears multiple times in word, then count each occurrence separately.

A substring is a contiguous sequence of characters in a string.

 

Example 1:

Input: word = "aba"
Output: 4
Explanation: The four wonderful substrings are underlined below:
- "aba" -> "a"
- "aba" -> "b"
- "aba" -> "a"
- "aba" -> "aba"

Example 2:

Input: word = "aabb"
Output: 9
Explanation: The nine wonderful substrings are underlined below:
- "aabb" -> "a"
- "aabb" -> "aa"
- "aabb" -> "aab"
- "aabb" -> "aabb"
- "aabb" -> "a"
- "aabb" -> "abb"
- "aabb" -> "b"
- "aabb" -> "bb"
- "aabb" -> "b"

Example 3:

Input: word = "he"
Output: 2
Explanation: The two wonderful substrings are underlined below:
- "he" -> "h"
- "he" -> "e"

 

Constraints:

    1 <= word.length <= 105
    word consists of lowercase English letters from 'a' to 'j'.

Intial Approach:- Randomly out of the box tried with 2D Array. IT worked but the overhead of 2D Array did not make much sense. Can we optimize on that?

![Screenshot 2023-10-01 at 8 40 23 PM](https://github.com/S2606/CodingQuestion/assets/18497513/30307e06-3d8d-4871-86ed-9e26b7c67d9f)

Code
```
class Solution {
    public long wonderfulSubstrings(String word) {
        long cnt[] = new long[1024], res = 0;
        int mask = 0;
        cnt[0] = 1;
        for(char c: word.toCharArray()){
            mask ^= (1<<(c-'a'));
            res += cnt[mask];
            for(int n=0;n<10;++n){
                res += cnt[mask ^ (1<<n)];
            }
            ++cnt[mask];
        }
        return res;
    }
}
```

Time complexity - O(n)
Space complexity - O(1)

