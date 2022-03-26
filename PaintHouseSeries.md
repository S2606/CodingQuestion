### The Question

There is a row of n houses, where each house can be painted one of three colors: red, blue, or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by an n x 3 cost matrix costs.

For example, costs[0][0] is the cost of painting house 0 with the color red; costs[1][2] is the cost of painting house 1 with color green, and so on...

Return the minimum cost to paint all houses.

Example 1:

```
Input: costs = [[17,2,17],[16,16,5],[14,3,19]]
Output: 10
Explanation: Paint house 0 into blue, paint house 1 into green, paint house 2 into blue.
Minimum cost: 2 + 5 + 3 = 10.
```

Approach:-

![Screenshot 2022-03-26 at 10 21 49 AM](https://user-images.githubusercontent.com/18497513/160225200-577aaafe-dcae-4a25-9c30-ddc1eeb3a036.png)

Lets Code

```
public int minCost(int[][] costs) {
    int m = costs.length;
    int n = costs[0].length;
    if(m==0){
       return 0;
    }
    
    for(int i=1;i<m;i++){
       costs[i][0] += Math.min(costs[i-1][1], costs[i-1][2]);
       costs[i][1] += Math.min(costs[i-1][0], costs[i-1][2]);
       costs[i][2] += Math.min(costs[i-1][1], costs[i-1][0]);
    }
    
    return Math.min(costs[i][0], Math.min(costs[i][1], costs[i][2]));
}
```

Time complexity - O(M) where M is number of rows
Space complexity - O(1)

### Lets make the question a bit harder

There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by an n x k cost matrix costs.

    For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on...

Return the minimum cost to paint all houses.

Example 1:

```
Input: costs = [[1,5,3],[2,9,4]]
Output: 5
Explanation:
Paint house 0 into color 0, paint house 1 into color 2. Minimum cost: 1 + 4 = 5; 
Or paint house 0 into color 2, paint house 1 into color 0. Minimum cost: 3 + 2 = 5.
```

![Screenshot 2022-03-26 at 4 14 07 PM](https://user-images.githubusercontent.com/18497513/160235955-92d1993b-7891-44e0-851e-811ead0b6f3d.png)

Lets Code
```
public int minCostII(int[][] costs) {
        int m = costs.length;
        int n = costs[0].length;
        if(m==0){
            return 0;
        }
        
        //int dp[][] = new int[m][n];
        int least = Integer.MAX_VALUE;
        int secondLeast = Integer.MAX_VALUE;
        for(int j=0;j<n;j++){
            if(costs[0][j]<=least){
                secondLeast = least;
                least = costs[0][j];
            } else if(costs[0][j]<=secondLeast) {
                secondLeast = costs[0][j];
            }
        }
        
        for(int i=1;i<m;i++){
            int newLeast = Integer.MAX_VALUE;
            int newSecondLeast = Integer.MAX_VALUE;
            for(int j=0;j<n;j++){
                if(least==costs[i-1][j]){
                    costs[i][j] = costs[i][j] + secondLeast;
                } else {
                    costs[i][j] = costs[i][j] + least;
                }
                
                if(costs[i][j]<=newLeast){
                    newSecondLeast = newLeast;
                    newLeast = costs[i][j];
                } else if(costs[i][j]<=newSecondLeast) {
                    newSecondLeast = costs[i][j];
                }
            }
            
            least = newLeast;
            secondLeast = newSecondLeast;
        }
        
        int ans = Integer.MAX_VALUE;
        for(int j=0;j<n;j++){
            ans = Math.min(ans, costs[m-1][j]);
        }
        
        return ans;
    }
```

Time complexity - O(nk) where k is total color count and n is no. of houses
Space complexity - O(1)

### Lets make the question a bit harder

There is a row of m houses in a small city, each house must be painted with one of the n colors (labeled from 1 to n), some houses that have been painted last summer should not be painted again.

A neighborhood is a maximal group of continuous houses that are painted with the same color.

    For example: houses = [1,2,2,3,3,2,1,1] contains 5 neighborhoods [{1}, {2,2}, {3,3}, {2}, {1,1}].

Given an array houses, an m x n matrix cost and an integer target where:

    houses[i]: is the color of the house i, and 0 if the house is not painted yet.
    cost[i][j]: is the cost of paint the house i with the color j + 1.

Return the minimum cost of painting all the remaining houses in such a way that there are exactly target neighborhoods. If it is not possible, return -1

Approach:-
![Screenshot 2022-03-26 at 6 09 43 PM](https://user-images.githubusercontent.com/18497513/160239844-cf24bc33-872d-413e-b7ef-30dc59aa7498.png)

```
final int MAX_COST = 1000001;
    public int minCost(int[] houses, int[][] cost, int m, int n, int target) {
        int[][][] memo = new int[m][target+1][n];
        
        for(int i=0;i<m;i++){
           for(int j=0;j<=target;j++){
                Arrays.fill(memo[i][j], MAX_COST);
            } 
        }
        
        for(int i=1;i<=n;i++){
            if(houses[0]==i){
                memo[0][1][i-1] = 0;
            } else if(houses[0]==0) {
                memo[0][1][i-1] = cost[0][i-1];
            }
        }
        
        for(int house = 1; house < m; house++){
            for(int neighbourhood = 1; neighbourhood <= Math.min(target, house+1); neighbourhood++){
                for(int color = 1; color <= n; color++){
                    if(houses[house]!=0 && color != houses[house]){
                        continue;
                    }
                    int currCost = MAX_COST;
                    for(int prevColor = 1; prevColor <= n; prevColor++){
                        if(color!=prevColor){
                            currCost = Math.min(currCost, memo[house-1][neighbourhood-1][prevColor-1]);
                        } else {
                            currCost = Math.min(currCost, memo[house-1][neighbourhood][color-1]);
                        }
                    }
                    
                    int costToPaint = houses[house]!=0 ? 0 : cost[house][color-1];
                    memo[house][neighbourhood][color-1] = costToPaint + currCost;
                }
          }
      }
        
      int minCost = MAX_COST;
      for(int color = 1; color <= n; color++){
          minCost = Math.min(minCost, memo[m-1][target][color-1]);
      }
        
      return minCost != MAX_COST ? minCost : -1;
    }
```

Time complexity - O(MTN^2)
Space Complexity - O(MTN)

Space complexity can be further reduced to O(TN) by using 2D Array(since only previous house data is required)
