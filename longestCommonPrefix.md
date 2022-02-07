## The question

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

- Example 1:

- Input: strs = ["flower","flow","flight"]
- Output: "fl"

Okay so the naive approach that comes to my mind

- Iterate all strings based on characters counter. But problem with this approach is that strings can be of different length.

So how can we make this better?

- Instead of going forward, lets go backward. Consider the first string as the prefix, chech the first occurance of it in next string. 
Till the time it does not find the index, trin the last character of the index.

Code

```
public String longestCommonPrefix(String[] strs) {
       if(strs.length==0) return "";
        String prefix = strs[0];
        for(int i=1; i<strs.length; i++){
            while(strs[i].indexOf(prefix)!=0){
                prefix = prefix.substring(0, prefix.length()-1);
            }
        }
        
        return prefix; 
    }
```

Time complexity - O(s) where s is the count of all characters of all strings
Space complexity - O(1)
