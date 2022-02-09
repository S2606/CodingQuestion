Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.


Initial apporach - calculate prefix sum for all elements, followed by backward traversal(i.e. if element is at nth position, after one 
pass of prefix sum calculation, traverse from 0 till n-1^th element, and the difference will give the maxumum subarray).

Time complexity - o(n^3) 
Space complexity - o(n)

Optimization - So this is a classic ase of kadane's algorithm

How it works is basically have a sum which checks that is it positively increasing or negatively dropping down the sum(there is no sense in adding two negative element
, they still stay as negative). if i were to give example

nums = [-2,1,-3,4,-1,2,1,-5,4]

ele = -2
max_so_far = 0 
max_ending = 0

ele = 1
max_so_far = 1
max_ending = 1

ele = -3
max_so_far = 1
max_ending = 0

ele = 4
max_so_far = 4
max_ending = 4

ele = -1
max_so_far = 4
max_ending = 3

ele = 2
max_so_far = 5
max_ending = 5

ele = 1
max_so_far = 6
max_ending = 6

ele = -5
max_so_far = 6
max_ending = 0

ele = 4
max_so_far = 6
max_ending = 4

public int maxSubArray(int[] nums) {
  int max_so_far = 0;
  int max_ending = 0;
  
  for(int num: nums){
     max_ending += num;
     if(max_so_far < max_ending){
          max_so_far = max_ending;
      } if(max_ending < 0){
          max_ending = 0;
      }
  }
  
  return max_so_far;
}
Time complexity - o(n) 
Space complexity - o(1)
