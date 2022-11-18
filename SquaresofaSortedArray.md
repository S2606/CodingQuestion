### The question

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example 1:

Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].

Example 2:

Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]

Approach:-

- Intial approach would have been, square the number, store it in array and just sort it. Time complexity in that case would be O(nlogn), space would be O(n). But what if I were to say that it can be done in O(n)?? Confused?? Hint:- The point is to not point towards the hint

![Screenshot 2022-11-18 at 11 37 43 AM](https://user-images.githubusercontent.com/18497513/202632824-54df27a8-9139-4d9a-976f-f563c63d9690.png)

Code:-

```
public int[] sortedSquares(int[] nums) {
    int n = nums.length;
    int ans[] = new int[n];
    int left = 0;
    int right = n-1;
    for(int i = n-1; i>=0; i--){
        int temp = 0;
        if(Math.abs(nums[left])<Math.abs(nums[right])){
            temp = nums[right];
            right--;
        } else {
            temp = nums[left];
            left++;
        }
        ans[i] = temp * temp;
    }

    return ans;
}
```

Time complexity - O(n)
Space complexity - O(n) if output array is considered else O(1)
