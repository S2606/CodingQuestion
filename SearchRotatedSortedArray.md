## The question

There is an integer array nums sorted in ascending order (with distinct values).
Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Initial approach:- sort the array, find target. Time complexity O(nlogn), Space complexity o(n)

## Bro they have hinted binary search, so lets stick to that

Okay but how to apply binary search in `sorted` rotated array?

In these types of arrays there can be two type of cases

![image](https://user-images.githubusercontent.com/18497513/154980440-e411b720-8f16-4fb9-953f-e41e3a4b0c9d.png)
 
- In this case if target is lower than mid, go towards the left else right

![image](https://user-images.githubusercontent.com/18497513/154980601-967a6250-4e11-48bd-808c-116f62d3e8d0.png)

- In this case if target is higher than mid, go towards the right else left

```
 public int search(int[] nums, int target) {
    int start = 0, end = target.length - 1;
    while(start < end){
      int mid = (end-start)/2;
      if(nums[mid]==target){
          return mid;
      } else if(nums[mid] >= nums[start]) {
        if(target >= nums[start] && target <= nums[mid]) end = mid-1;
        else start = mid+1;
      } else {
        if(target <= nums[end] && target >= nums[mid]) start = mid+1;
        else end = mid-1;
      }
    }
    return -1;
 }
```

Time complexity - O(n) Space complexity - O(1)
