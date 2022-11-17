### The question

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [1,3,5,6], target = 5
Output: 2

Example 2:

Input: nums = [1,3,5,6], target = 2
Output: 1

Example 3:

Input: nums = [1,3,5,6], target = 7
Output: 4


Approach:-

![Screenshot 2022-11-17 at 12 04 37 PM](https://user-images.githubusercontent.com/18497513/202373710-a8fd66e2-654a-4544-97b0-7cddc44f4869.png)

Code:-

```
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(nums[mid]==target) return mid;
            else if(nums[mid]<target) left = mid+1;
            else right = mid-1;
        }
        return left;
    }
}
```

Time complexity - O(log n) why? By using master's theorm T(N)=aT(N/b)+Θ(N^d). The equation represents dividing the problem up into a subproblems of size N/b​ in Θ(N^d) time. Here at each step there is only one subproblem i.e. a = 1, its size is a half of the initial problem i.e. b = 2, and all this happens in a constant time i.e. d = 0. As a result, log⁡ a to the base b=d and hence we're dealing with case 2 that results in O(n^log⁡ a to the base b log ^⁡d+1 N) = O(log⁡N) time complexity. [Link to reason](https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms)#Case_2_example)

Space complexity - O(1)
