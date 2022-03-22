## The question

There are n points on a road you are driving your taxi on. The n points on the road are labeled from 1 to n in the direction you are going, and you want to drive from point 1 to point n to make money by picking up passengers. You cannot change the direction of the taxi.
The passengers are represented by a 0-indexed 2D integer array rides, where rides[i] = [starti, endi, tipi] denotes the ith passenger requesting a ride from point starti to point endi who is willing to give a tipi dollar tip.
For each passenger i you pick up, you earn endi - starti + tipi dollars. You may only drive at most one passenger at a time.

Given n and rides, return the maximum number of dollars you can earn by picking up the passengers optimally.

Note: You may drop off a passenger and pick up a different passenger at the same point.

Example:
```
Input: n = 20, rides = [[1,6,1],[3,10,2],[10,12,3],[11,12,2],[12,15,2],[13,18,1]]
Output: 20
Explanation: We will pick up the following passengers:
- Drive passenger 1 from point 3 to point 10 for a profit of 10 - 3 + 2 = 9 dollars.
- Drive passenger 2 from point 10 to point 12 for a profit of 12 - 10 + 3 = 5 dollars.
- Drive passenger 5 from point 13 to point 18 for a profit of 18 - 13 + 1 = 6 dollars.
We earn 9 + 5 + 6 = 20 dollars in total.
```

Approach: 

![Screenshot 2022-03-22 at 10 49 55 PM](https://user-images.githubusercontent.com/18497513/159538620-2885b03e-c796-4152-844b-8b0cfca0e523.png)

From what i can understand, applying greedy will not help in getting optimal solution. Can also not think of finding all 
possible combinations can have large possibilities. So does this qualify as a DP problem?

```
1) Identify if it is a DP problem
  1.1) Does it statisfy Optimal Substructure Property?
      Lets say that L(i) denotes the maximum earnings ending till point i
      L(i) = Math.max(L(i), L(start) + endtrip-startrip+tip);
      # Note start was an end point for some cases. 
      
  1.2) Does it statisfy Overlapping Subproblem Property?
     - Can a recursion function br written? Yes
       int rec(int [][] earn, int[] arr, int i, int m){
            if(i>=m){
              return 0;
            }
            
            return Math.max(L(arr[i]), L(start) + end-start+tip);
       }
       As you can see multiple times values are being recalculated, can be saved using an 1d-array called dp 
       
2) Decide a state expression with least parameters
   dp[i] this means maximum dollars till point i;
   
3) Formulate state relationship
   dp[i] = Math.max(dp[i], dp[start] + end-start+1);

4) Memonize
   Store it in 1d Array
   
Some optimizations that can be done, sort the records based on ending point
```

Lets code
```
public long maxTaxiEarnings(int n, int[][] rides) {
    Arrays.sort(rides, (a, b) -> Integer.compsre(a[1], b[1]));
    long dp[] = new long[n+1];
    int k = 0;
    
    for(int i=1; i<=n; i++){
      dp[i] = dp[i-1];
      while(k<dp.length && i == rides[k][1]){
        int [] ride = rides[k++];
        dp[i] = Math.max(dp[i], dp[ride[0]] + ride[1] - ride[0] + ride[2]);
      }
    }
    
    return dp[n];
}
```
Time complexity- O(n+klogk) where k is array length
space complexity - O(n)
