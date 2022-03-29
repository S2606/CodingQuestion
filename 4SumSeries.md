### The question

Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:
```
    0 <= a, b, c, d < n
    a, b, c, and d are distinct.
    nums[a] + nums[b] + nums[c] + nums[d] == target
```
You may return the answer in any order.

```
Constraints:
    1 <= nums.length <= 200
    -109 <= nums[i] <= 109
    -109 <= target <= 109
```

Example 1:

```
Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

Approach:-

![Screenshot 2022-03-29 at 11 57 00 AM](https://user-images.githubusercontent.com/18497513/160547179-01d49a06-afa0-4375-b17a-63325807ecd3.png)

Lets Code
```
public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        return KSum(nums, target, 0, 4);
  }

  public List<List<Integer>> KSum(int[] nums, int target, int start, int k){
      List<List<Integer>> result = new ArrayList();

      if (start == nums.length) {
          return result;
      }

      int average_value = target/k;

      if(nums[start]>average_value || average_value>nums[nums.length-1]){
          return result;
      }

      if(k==2){
          return twoSum(nums, target, start);
      }

      for(int i=start; i<nums.length; i++){
          if(i==start || nums[i-1]!=nums[i]){
              for(List<Integer> subSet: KSum(nums, target-nums[i], i+1, k-1)){
                  result.add(new ArrayList<>(Arrays.asList(nums[i])));
                  result.get(result.size()-1).addAll(subSet);
              }
          }
      }

      return result;
  }

  public List<List<Integer>> twoSum(int[] nums, int target, int start){
      List<List<Integer>> res = new ArrayList<>();
      int low = start, high = nums.length-1;
      while(low<high){
          if(nums[low]+nums[high]<target || (low > start && nums[low-1]==nums[low])){
              ++low;
          } else if(nums[low]+nums[high]>target || (high < nums.length-1 && nums[high]==nums[high+1])){
              --high;
          } else {
              res.add(Arrays.asList(nums[low++], nums[high--]));
          }
      }

      return res;
  }
```

Time complexity - O(N^k-1) where K is the sum count
Space complexity - O(N)
