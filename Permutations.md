## The question

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Example 1:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Initial approach - create all permutations via multiple for loops, time complexity O(N!)

Actually i guess we kinda need to do the above mentioned approach, its just that you do not need multiple for loops, but backtracking can help. 
In backtracking, via recursions one can `backtrack` to the previous state for generating the next permutation, how?? lets find out

```
public List<List<Integer>> permute(int[] nums) {
   if(nums.length()==0){
      return new ArrayList();
   }
  
   List<List<Integer>> res= new ArrayList<>();
   backtrack(nums, 0, res);
}
  
public void backtrack(int[] nums, int start, List<List<Integer>> res){
  if(start==nums.length){
      ArrayList<Integer> list = new ArrayList<Integer>();
      for(int n: nums){
          list.add(n);
      }
      if(!res.contains(temp)){
          res.add(temp);
      }
  } else {
     for(int i=start; i<nums.length(); i++){
         swap(arr, start, i);
         backtrack(nums, start+1, res);
         swap(arr, i, start);
     }
  }
}
```

- Time complexity - between O(N X N!) and O(N!) For more analysis check [this](https://leetcode.com/problems/permutations/solution/)
- Space - O(N!)

