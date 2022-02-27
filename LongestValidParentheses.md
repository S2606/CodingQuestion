## The question

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

Example 1:

```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
```

Brute force:- generate all possible combinations, check their validity by using stack. Time complexity - O(n^3)

```
1) Identify if it is a DP problem
  1.1) Does it statisfy Optimal Substructure Property?
      Let array dp[0,... n-1] where dp[i] means longest valid parentheses substring till character position i
      if s.charAt(i) == `)` and s.charAt(i-1) == `(` else dp[i] = dp[i-2]+2 this would mean skipping `()`
      if s.charAt(i) == `)` and s.charAt(i-1) == `)` and s.charAt(i-dp[i-1]-1) == `(` then dp[i] = dp[i-1]+dp[i-dp[i-1]-2]+2 why??
      because we know that the i-1th string could have its own longest valid parenthesis substring(eg:- `(())`). 
      So i-dp[i-1]-2 means skipping the two pairs and substring in between eg:-`(sub_str)`
      
  1.2) Does it statisfy Overlapping Substructure Property?
      - Can a recursion related solution be made from this? Yes
      ```
      int max = 0;
      int rec(char[] A, int m, int i){
          if(A[i]==')'){
            if(A[i-1]=='('){
              max = Math.max(max, (i>=2 ? rec(A, m, i-2) : 0) + 2);
            } else {
              int temp = rec(A, m, i-1);
              max = Math.max(max, (i-temp>=2 ? temp-rec(A, m, i-temp-2) : 0) + 2);
            }
          }
          return max;
      }
      ```
      As you can see, if recursion tree is plotted, there are many overlapping values being recalculated, hence can be stored in an array
```

```
public int longestValidParentheses(String s) {
    int maxans = 0;
    int dp[] = new int[s.length()];
    for(int i=1; i<s.length(); i++){
        if(s.charAt(i)==')'){
            if(s.charAt(i-1)=='('){
                dp[i] = (i>=2 ? dp[i-2]:0)+2;
            } else if(i-dp[i-1]>0 && s.charAt(i-dp[i-1]-1) == '(') {
                dp[i] = dp[i-1] + (i-dp[i-1]>=2 ? dp[i-dp[i-1]-2] : 0) + 2;
            }
            maxans = Math.max(maxans, dp[i]);
        }
    }
    return maxans;
}
```

Time complexity - O(n)
Space complexity - O(n)

Space complexity can further be optimized since we care about only the size. Can use two pointers- left and right and can scan on both front and back side. 
if left == right then max = Math.max(max, 2*left), if(right>left) mark both as zero(this is ltr scan, will do vice-versa for rtl scan)

