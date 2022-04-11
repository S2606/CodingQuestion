### The question

You are given three positive integers: n, index, and maxSum. You want to construct an array nums (0-indexed) that satisfies the following conditions:

    nums.length == n
    nums[i] is a positive integer where 0 <= i < n.
    abs(nums[i] - nums[i+1]) <= 1 where 0 <= i < n-1.
    The sum of all the elements of nums does not exceed maxSum.
    nums[index] is maximized.

Return nums[index] of the constructed array.

Note that abs(x) equals x if x >= 0, and -x otherwise.

Example 1:

```
Input: n = 4, index = 2,  maxSum = 6
Output: 2
Explanation: nums = [1,2,2,1] is one array that satisfies all the conditions.
There are no arrays that satisfy all the conditions and have nums[2] == 3, so 2 is the maximum nums[2].
```

Approach:-

![Screenshot 2022-04-11 at 11 19 06 AM](https://user-images.githubusercontent.com/18497513/162672785-e825c2bc-5185-4a91-93f9-08fe60939c1a.png)

Lets code
```
public int maxValue(int n, int index, int maxSum) {
    maxSum -= n
    int left = 0, right = maxSum;
    while(left<right){
        int mid = (left+right+1)/2 // why +1?? since we want to find last valid element
        if(test(n, index, mid)<=maxSum){
            left = mid;
        } else {
            right = mid-1;
        }
    }
    return left+1;
}

public long test(int n, int index, int mid){
    int b = Math.max(a-index, 0);
    long res = (long)(a+b)*(a-b+1)/2;
    b = Math.max((a-((n-1)-index)), 0);
    res += (long)(a+b)*(a-b+1)/2;
    return res-a;
}
```

Time complexity - O(log(maxSum)) since n here is maxSum
Space complexity - O(1)
