## The question

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Example 1:

Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]

Initial approach:-  First can think of generating manually. Time complexity - o(2^(2*n)). 
Repeated pattern generation, Backtracking to the rescue, but how?

so what we can do is take to variables, open and close(both int), and first fill with open as counter, this is followed bu taking open as a counter for close.

```
public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<String>();
    backtrack(result, "", 0, 0, n);
}

public void backtrack( List<String> result, String temp, int open, int closed, int max){
     if(open+closed==max*2){
         result.add(temp);
         return;
     }
     
     if(open<max){
        temp.add("(");
        backtrack(result, temp, open+1, closed, max);
        temp.deleteCharAt(temp.length() - 1);
     }
     
     if(closed<open){
        temp.add(")");
        backtrack(result, temp, open, closed+1, max);
        temp.deleteCharAt(temp.length() - 1)
     }
```

Time complexity - O(4^N/b^(n*0.5^M) Similar to catalan numbers
Space complexity - same

