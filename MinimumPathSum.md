## The question

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/157808744-acc342f4-422a-4859-bff7-a7105c3a1535.png)

```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

Approach:- Thought of usign greedy, will not work in the above example. Don't think path traversal is a good idea, given it can have humungous number 
of paths possible on larger square counts. 

Can this be solved by DP?

```
1) Identify if it is a DP problem
  1.1) Does it statisfy Optimal Substructure Property?
      Lets say that L(i, j) denotes the minimum path sum from point (i,j) till (m-1, n-1). so in order to calculate the sum
      L(i, j) = arr[i][j] + min(L(i+1, j), L(i, j+1));
  1.2) Does it statisfy Overlapping Subproblem Property?
     - Can a recursion function br written? Yes
       int rec(int [] path, int i, int j, int m, int n){
            if(i>=m || j>=n){
              return 0;
            }
            
            return path[i][j] + Math.min(rec(path, i+1, j, m, n), rec(path, i, j+1, m, n));
       }
       As you can see multiple times values are being recalculated, can be saved using an 2d-array called dp 
       
2) Decide a state expression with least parameters
   dp[i][j] this means minimum path distance from point (i,j) till (m-1, n-1)
   
3) Formulate state relationship
   dp[i][j]  = path[i][j] + Math.min(dp[i+1][j], dp[i][j+1]

4) Memonize
   Store it in 2d Array
```

I guess code is the only thing that is left

```
public int minPathSum(int[][] grid) {
  int m = grid.length;
  int n = grid[0].length;
  int dp[][] = new int[m][n];

  for(int i=m-1; i>=0; i--){
    for(int j=n-1; j>=0; j--){
      if(i==m-1 && j!=n-1){
        dp[i][j] = grid[i][j] + dp[i][j+1];
      } else if(i!=m-1 && j==n-1){
        dp[i][j] = grid[i][j] + dp[i+1][j];
      } else if(i!=m-1 && j!=n-1){
        dp[i][j] = grid[i][j] + Math.min(dp[i+1][j], dp[i][j+1]);
      } else {
        dp[i][j] = grid[i][j];
      }
    }
  }
  reutrn dp[0][0];
}
```
This can have space complexity as O(1) if original matrix is not needed further

Can we move this into an 1D array answer is yes. how? 

![Screenshot 2022-03-12 at 4 22 58 PM](https://user-images.githubusercontent.com/18497513/158015150-2340cb2c-893f-4fcc-a8a9-9bea77a8688d.png)

```
public int minPathSum(int[][] grid) {
  int m = grid.length;
  int n = grid[0].length;
  int dp[] = new int[n];

  for(int i=m-1; i>=0; i--){
    for(int j=n-1; j>=0; j--){
      if(i==m-1 && j!=n-1){
        dp[j] = grid[i][j] + dp[j+1];
      } else if(i!=m-1 && j==n-1){
        dp[j] = grid[i][j] + dp[j];
      } else if(i!=m-1 && j!=n-1){
        dp[j] = grid[i][j] + Math.min(dp[j], dp[j+1]);
      } else {
        dp[j] = grid[i][j];
      }
    }
  }
  reutrn dp[0];
}
```
