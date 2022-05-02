You are given n balloons, indexed from 0 to n - 1. Each balloon is painted with a number on it represented by an array nums. You are asked to burst all the balloons.

If you burst the ith balloon, you will get nums[i - 1] * nums[i] * nums[i + 1] coins. If i - 1 or i + 1 goes out of bounds of the array, then treat it as if there is a balloon with a 1 painted on it.

Return the maximum coins you can collect by bursting the balloons wisely.

Example 1:

```
Input: nums = [3,1,5,8]
Output: 167
Explanation:
nums = [3,1,5,8] --> [3,5,8] --> [3,8] --> [8] --> []
coins =  3*1*5    +   3*5*8   +  1*3*8  + 1*8*1 = 167
```

Approach:-

![Screenshot 2022-05-02 at 11 39 28 AM](https://user-images.githubusercontent.com/18497513/166191834-8325e355-2f01-4d16-9952-8603a3b83bfa.png)


Lets code:-

```
public int maxCoins(int[] nums) {
    int n = nums.length;
    if(n==0){
        return 0;
    }
    int dp[][] = new int[n][n];

    for(int len=1; len <= n; len++){
        for(int i=0;i<=n-len;i++) {
            int j = i+len-1;
            for(int k=i; k<=j; k++){
                int leftVal = 1;
                int rightVal = 1;

                if(i!=0){
                    leftVal = nums[i-1];
                }

                if(j!=n-1){
                    rightVal = nums[j+1];
                }

                int before = 0;
                int after = 0;

                if(i!=k){
                    before = dp[i][k-1];
                }

                if(k!=j){
                    after = dp[k+1][j];
                }

                dp[i][j] = Math.max(before + (leftVal * nums[k] * rightVal) + after, dp[i][j]);
            }
        }
    }

    return dp[0][n-1];
}
```

Time complexity - O(n^2)
Space complexity - O(n^2)
