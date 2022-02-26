### The question

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

A palindrome string is a string that reads the same backward as forward.

Example 1:
```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

Initial approach:- create all possible combinations of characters based on points of separation using backtracking + dfs. Time complexity - O(N*2^N)

```
public List<List<String>> partition(String s) {
     List<List<String>> result = new ArrayList<>();
     dfs(0, result, new ArrayList<String>(), s);
     return result;
}

public void dfs(int start, List<List<String>> result, ArrayList<String> currentList, String s){
    if(start>=s.length()) result.add(new ArrayList<String>(currentList);
    for(int end = start; end < s.length(); end++){
        if(isPalindrome(s, start, end)){
           currentList.add(s.subString(start, end+1));
           dfs(end+1, result, currentList, s);
           currentList.remove(currentList.size()-1);
        }
    }
    
}

public boolean isPalindrome(String s, int start, int end){
  while(start<end){
      if(s.charAt(start++)!=s.charAt(end--)) return false;
  }
  return true;
}
```

Time complexity - O(N*2^N) where N is no. of characters. Worst case scenario wouls be string like "aaaa".
Space complexity - O(N)

There is also a solution involving DP but not considering here for the fact that space complexity would increase to O(N^2)
