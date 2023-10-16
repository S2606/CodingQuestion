### The question

Given an integer array nums, you need to find one continuous subarray such that if you only sort this subarray in non-decreasing order, then the whole array will be sorted in non-decreasing order.

Return the shortest such subarray and output its length.

Example 1:

Input: nums = [2,6,4,8,10,9,15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.

Example 2:

Input: nums = [1,2,3,4]
Output: 0

Example 3:

Input: nums = [1]
Output: 0

Initial approach:- Check the point at which cliff is happening. If found, set start and end. Almost like selection sort, problem being it needs two for loops in order to consider all cases. Time complexity being O(n^2). In order to optimize this can we think of executing it in one loop? Doesnt matter if it gets executed two times separately right? It can be done using stack data structure. How?

![Screenshot 2023-10-16 at 6 50 46 AM](https://github.com/S2606/CodingQuestion/assets/18497513/ef0e82aa-3af0-4999-a96f-4d1f7baae264)

Code:- 
```
public int findUnsortedSubarray(int[] nums) {
        int start = nums.length;
        int end = 0;
        Stack<Integer> stk = new Stack<Integer>();
        for(int i=0;i<nums.length;i++){
            while(!stk.isEmpty() && nums[stk.peek()]>nums[i]){
                start = Math.min(start, stk.peek());
                stk.pop();
            }
            stk.push(i);
        }
        
        for(int i=nums.length-1;i>=0;i--){
            while(!stk.isEmpty() && nums[stk.peek()]<nums[i]){
                end = Math.max(end, stk.peek());
                stk.pop();
            }
            stk.push(i);
        }
        return end-start < 0 ? 0 : end-start+1;
    }
```

Time complexity - O(n)  Space complexity - O(n)

This is good. What if we were told to optimize space? I guess we can since we do not care about the flow of element insertion and deletion in stack right? What if stack was replaced with simple variables?

Code:-
```
public int findUnsortedSubarray(int[] nums) {
        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
        boolean flag = false;
        for(int i=1;i<nums.length;i++){
            if(nums[i]<nums[i-1]){
                flag = true;
            }
            if(flag){
                min = Math.min(min, nums[i]);
            }
        }
        flag = false;
        for(int i=nums.length-2;i>=0;i--){
            if(nums[i]>nums[i+1]){
                flag = true;
            }
            if(flag){
                max = Math.max(max, nums[i]);
            }
        }
        
        int l, r;
        for(l=0;l<nums.length;l++){
            if(min<nums[l])
                break;
        }
        
        for(r=nums.length-1;r>=0;r--){
            if(max>nums[r])
                break;
        }
        
        return r-l<0?0:r-l+1;
    }
```
Time complexity - O(n)  Space complexity - O(1)
