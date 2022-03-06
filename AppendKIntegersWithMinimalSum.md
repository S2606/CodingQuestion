## The question

You are given an integer array nums and an integer k. Append k unique positive integers that do not appear in nums to nums such that the resulting total sum is minimum.

Return the sum of the k integers appended to nums.


Example 1:

```
Input: nums = [1,4,25,10,25], k = 2
Output: 5
Explanation: The two unique positive integers that do not appear in nums which we append are 2 and 3.
The resulting sum of nums is 1 + 4 + 25 + 10 + 25 + 2 + 3 = 70, which is the minimum.
The sum of the two integers appended is 2 + 3 = 5, so we return 5.
```

Intial Approach:- Iterate through every element(after sorting), find unique elements. will give TLE.

How can we optimize?

![LeetcodeContestAddK](https://user-images.githubusercontent.com/18497513/156915425-5a667e77-4c5b-40ff-b12b-21a6156e944b.png)

```
public long minimalKSum(int[] nums, int k) {
    Arrays.sort(nums);
    Set<Integer> set = new HashSet<Integer>();
    long sum = 0;
    for(int num: nums){
      if(!set.contains(num) && num <= k){
          k++;
          sum += num;
      }
      set.add(num);
    }
    
    long resp = (long)(1+k)*k/2 - sum;
    return resp;
}
```

Time complexity - O(nlogn)
Space complexity - O(n)
