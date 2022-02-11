## Maximum Product Subarray

Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

A subarray is a contiguous subsequence of the array.

Example 1:

Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.


Initial approach - thought of simp1e pass loop, followed by checks(multiply number, check with largest). 
Problem is does it work in the case all numbers are negative?

in order to solve this, need to upgrade the current process. How?? By calculating minimum amount till that point, and use that for handling negative number cases.

nums = [2,3,-2,4]


1) max_so_far = 2;
   min_so_far = 2;
   final_max = 2;

2) temp = 2;
   max_so_far = 6;
   min_so_far = 3;
   final_max = 6;

3) temp = -2;
   max_so_far = 6;
   min_so_far = 3;
   final_max = -2;

4) temp = 3;
   max_so_far = 6;
   min_so_far = 3;
   final_max = -2;

Code:-

```
public int maxProduct(int[] nums) {
   if(nums.length==0){
            return 0;
        }
    int max_so_far = nums[0];
    int min_so_far = nums[0];
    int finalAns = nums[0];
    
    for(int i=1;i<nums.length;i++){
        temp = max_so_far;
         max_so_far  = Math.max(Math.max(max_so_far*nums[i], nums[i]*mun_so_far), nums[i]);
         min_so_far  = Math.min(Math.min(temp*nums[i], nums[i]*mun_so_far), nums[i]);
         if(finalAns < max_so_far){
             finalAns = max_so_far;
         }
    }
    
    return finalAns;
}
```

Time complexity - O(n)
Space complexity - O(1)    
