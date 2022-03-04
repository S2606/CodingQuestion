You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Example 1:

```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

Approach :- Initially one can simply just calculate all possibilities. Instead this seems to be a classic case of dp. why?

```
1) Identify if it is a DP problem
  1.1) Does it statisfy Optimal Substructure Property?
    - Let A[i] means no. of distinct ways to climb the stairs. Therefore
      A[i] = A[i-1] + A[i-2]
  1.2) Does it have Overlapping Subproblem?
    - Can a recursive function be written? Yes
      ```
      public int recur(int i){
        if(i<=0){
          return 0;
        }
        
        return recur(i-1) + recur(i-2);
      }
      ```
```

Okay so only last elements can be stored for calculating number of distinct steps. I guessed you missed it but its completely realted to fibonacci series!

```
public int climbStairs(int n) {
  if(n==1){
    return 1;
  }
  
  int first = 1;
  int second = 2;
  for(int i=3; i<=n; i++){
    int third = first + second;
    first = second;
    second = third;
  }
  return second;
}
```

Time Complexity - O(N)
Space Complexity - O(1)
