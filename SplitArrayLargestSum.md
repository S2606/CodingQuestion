### The question

Given an array nums which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these m subarrays.

Example 1:

```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

Approach:-

![Screenshot 2022-04-12 at 9 05 14 PM](https://user-images.githubusercontent.com/18497513/162999835-a8fee2fe-cf2e-4a91-968e-f9103e058fd1.png)

Lets code:-

```
public int splitArray(int[] nums, int m) {
    long left = 0, right = 0;
    for(int num: nums){
        left = Math.max(left, num);
        right += num;
    }
    long ans = right;
    while(left<=right){
        long mid = left+(right-left)/2;
        long tmpCount = 1, sum = 0;
        for(int num: nums){
            if(sum+num>mid){
                tmpCount++;
                sum = num;
            } else {
                sum += num;
            }
        }

        if(tmpCount>m){
            left = mid + 1;
        } else {
            ans = Math.min(ans, mid);
            right = mid-1;
        }
    }

    return (int) ans;
}
```

Time complexity - O(nlog(S)) where S is sum of array
Space complexity - O(1)
