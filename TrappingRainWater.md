## The question

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/165003292-d8ae3e0b-814f-42b5-8a87-88567d7705c2.png)

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section)
are being trapped.
```

Approach:- From what I can understand, need to know the difference of length of bars on both sides in which maximum water can get filled. But it also
provides a hint of considering division into subproblem. Lets validate with a template.

```
First of all why DP?
The brute force solution basically is find left_max and right_max from a point. This on find for all_points can have a time complexity of O(n^2). Can this
be memonized in order to prevent re-calculations

1) Does it statisfy Optimal Substructure Property?
  Lets suppose A[0..m-1] contains maximum capacity of water filled till block m. In order to find maximum water filled, the formula can be as follows
    if length of m-1th block <= length of m+1th block then A[m] = A[m-1]th + ((length of m+1th block - length of m-1th block) - length of mth block)
    else A[m] = ((length of m+1th block - length of m-1th block) - length of mth block)
  But this approach will fail because 
  1) Maximum left/right can be more than distance 1
  2) Can get negative answer
 Instead lets store only two things that matter the most, left_max and right_max, and then apply(min(left, right)-current. complexity is O(N) for 
   both time and space
  
It seems we can have a better solution than DP. since we do not care about all left, right maxes but just the recent ones. How about we use pointers?
How:-
  make two pointers left and right
     while left<right
        if height[right] > height[left]
            if height[left] >= left_max
               left_max = height[left]
            else
               answer += left_max - height[left]
            left+=1
        if height[right] < height[left]
             if height[right] >= right_max
               right_max = height[right]
            else
               answer += right_max - height[right]
            right+=1
 time complexity - O(n) space complexity - O(1)
```
