### The question

You are given a 0-indexed integer array nums. You have to partition the array into one or more contiguous subarrays.

We call a partition of the array valid if each of the obtained subarrays satisfies one of the following conditions:

    The subarray consists of exactly 2 equal elements. For example, the subarray [2,2] is good.
    The subarray consists of exactly 3 equal elements. For example, the subarray [4,4,4] is good.
    The subarray consists of exactly 3 consecutive increasing elements, that is, the difference between adjacent elements is 1. For example, the subarray [3,4,5] is good, but the subarray [1,3,5] is not.

Return true if the array has at least one valid partition. Otherwise, return false.

Example

```
Input: nums = [4,4,4,5,6]
Output: true
Explanation: The array can be partitioned into the subarrays [4,4] and [4,5,6].
This partition is valid, so we return true.
```

Approach :-

![Screenshot 2022-08-29 at 11 42 25 AM](https://user-images.githubusercontent.com/18497513/187134598-5d9baf29-d185-48c2-93ed-e8b0ce81adbf.png)

Code:-

```
public boolean validPartition(int[] nums) {
    int n = nums.length;

    if(n==2){
        return nums[0] == nums[1];
    }

    boolean [] dp = new boolean[n+1];
    dp[1] = nums[0] == nums[1];
    dp[2] = ((nums[0] == nums[1])&&(nums[1] == nums[2]) || (nums[0]+1 == nums[1])&&(nums[1]+1 == nums[2]));

    for(int i=3; i<n; i++){
        if(nums[i]==nums[i-1]){
            dp[i] |= dp[i-2];
        } if((nums[i] == nums[i-1])&&(nums[i-1] == nums[i-2])){
            dp[i] |= dp[i-3];
        } if((nums[i]-1 == nums[i-1])&&(nums[i-1]-1 == nums[i-2])){
            dp[i] |= dp[i-3];
        }
    }

    return dp[n-1];
}
```

- Time complexity - O(n)
- Space complexity - O(n)

But can we optimize it more? Yes. As one can see the max we go is two steps behind. so can we think something related to this? yeah, we can have something of a fixed size dp array(4 in our case). This can be traversed in a circular fashion

![Screenshot 2022-08-29 at 12 54 18 PM](https://user-images.githubusercontent.com/18497513/187146494-060f155c-3b6c-493c-9b7f-06c77b6aadb9.png)

Code:-

```
public boolean validPartition(int[] n) {
    boolean dp[] = {true, false, n[0]==n[1], false};
    for(int i=2;i<n.length;i++){
        boolean two = n[i]==n[i-1];
        boolean three = (two && n[i] == n[i - 2]) || (n[i] - 1 == n[i - 1] && n[i] - 2 == n[i - 2]);
        dp[(i+1)%4] = (two&&dp[(i-1)%4]) || (three&&dp[(i-2)%4]);
    }

    return dp[n.length%4];
}
```

- Time complexity - O(n)
- Space complexity - O(1)
