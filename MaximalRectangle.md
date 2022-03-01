## The question

Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/155729065-775e64ae-e39e-462a-aa56-854d6cd3223d.png)

```
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.
```
Initial approach, find all combinations. Time complexity O(N^3 * M^3)

This seems to be a case of DP? Why?
```
1) Identify if it is a DP problem
  1.1) Does it statisfy Optimal Substructure Property?
      Yes, lets suppose there is an array row[], which represents a row in matrix provided above. So what in recurrence relation?
      ```
        row[i] = 1+ row[i-1] if row[i] == 1 else row[i] = 0
      ```
      Okay so now in order to find maximal rectangle, we have found the breadth. now lets find out the length. how so in order to do that we need to 
      traverse upwards to find the maximum possible length. Okay so if dp[][] is a 2d-array in which dp[i][j] denotes maximal width at point(i, j), 
      then formula will be
      ```
        width = Math.min(width, dp[k][j]); where k: i->0(this means we are searching lengthwise(bottm to top)
        area = Math.max(area, i-k+1);
      ```
  1.2) Does it satisfy Overlapping Subproblem Property?
      - Can a recursion related solution be made from this? Yes
        ```
        Quite difficult and non-intuitive hence not considering
        ```
```

Okay, since we are not considering dp, what else do you have on top of your mind? Dou remember larget rectangle histogram?? Can we use that here?

```
public int largRecHist(int[] dp){
  Stack<Tnteger> stk = new Stack<>();
  stk.add(-1);
  int maxarea = 0;
  for(int i=0;i<dp.length;i++){
    while(stk.peek()!=1 && dp[stk.peek()] > dp[i]){
        int ele = stk.pop();
        maxarea = Math.max(maxarea, (i-stk.peek()-1)*(dp[ele]);
    }
    
    stk.add(i);
  }
  
  return maxarea;
}

public int maximalRectangle(char[][] matrix) {
    if (matrix.length == 0) return 0;
    int maxarea = 0;
    int[] dp = new int[matrix[0].length];

    for(int i = 0; i < matrix.length; i++) {
        for(int j = 0; j < matrix[0].length; j++) {
            dp[j] = matrix[i][j] == '1' ? 1 + dp[j-1] : 0;
        }
        maxArea = Math.max(maxArea, largRecHist(dp));
    }
    
    return maxArea;
} 
```

Time complexity - O(NM) actually its O(N * 2M)
Space complexity - O(NM)
