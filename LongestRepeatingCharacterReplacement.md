## The question

You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

Example 1:

```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```

Approach:- So we need to basically **slide towards right** in order to find the longest substring after doing k operations, along with consideration of not counting already similar elements.

can think of sliding window, wherein first we can expand towards right, and will stop only if the substring has already done k operations(how can we know this?).

```
Lets suppose start and end are two pointers that point to start and end of a substring. 
Length of substring is end-start+1.

Now lets say maxRep contains number of already repeated character in thsat substring(B in the below example), 
can we say that end-start+1-maxRep denotes number ofoperations that are to be done in order to create 
longest substring of same characters(isn't that supposed to be k?)
```

Can use HashMap for maxRep, but a point to remember is that values in the map will also **slide towards right**, for removing unwanted ones that do not belong in currrent substring

![Screenshot 2022-03-16 at 10 24 55 AM](https://user-images.githubusercontent.com/18497513/158519309-70951014-dbde-4a23-a970-f375cd2fd138.png)

Lets code
```
 public int characterReplacement(String s, int k) {
    int maxRepeat = 0;
    int start = 0;
    int longest = 0;
    HashMap<Character, Integer> map =  new HashMap();
    for(int end=0;end<s.length();end++){
        char right = s.charAt(end);
        map.put(right, map.getOrDefault(right, 0)+1);
        maxRepeat = MAth.max(maxRepeat, mao.get(right));
        if(end-start+1-maxRepeat > k){
          char left = s.charAt(start);
          map.put(left, map.get(left)-1);
          if(map.get(left)==0){
             map.remove(left);
          }
          start++;
        }
        longest = Math.max(longest, end-start+1);
    }
    
    return longest;
 }
```

Time complexity - O(n)
Space complexity - O(n)
