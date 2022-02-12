## The question

Given an array of integers nums and an integer k, return the total number of continuous subarrays whose sum equals to k.

Example 1:

Input: nums = [1,1,1], k = 2
Output: 2

Initial approach - two for loops, one iterating from start, other from next element of start till end. 

Time complexity - O(n^3) - n of outer for loop, inner for loop goes from (n-1) till 1
    
       (n-1) + (n-2) + ... + 1

       on finding arithmetic sum, the complexity comes out to be ~O(n^2)

Better approach - If a sum is already calculated, why not store it? Could be used to find k. How?

       1,2,3,4
       sum till 2 - 3
       sum till 4 - 10
       if we do 10-3 = 7, this means 7 is sum of subarray [3,4]

Storage mechanism? Can use another array but time complexity still stays as O(n^2). So how do we ensure that access to these elements stay at O(1)? 
- Enter HashMaps

In HashMaps, we shall store key as sum, and count of occurence of that sum as value. Why? so that count of subarray is considered for all subarrays of the same value.
Can possibly have two pairs of same value, both are potential candidates for formation of subarray

sum[i]-sum[j] =k. Therefore sum[i]-k=sum[j]

Code 

```
public int subarraySum(int[] nums, int k) {    
    int sum, count;
    HashMap<int, int> map = new HashMap();
    map.add(0, 1);
    for(int i=0;i<nums.length;i++){
       sum+=nums[i];
       if(map.contains(sum-k)){
          count+=map.get(sum-k);
       }
       map.put(sum, map.getOrDefault(sum, 0)+1);
    }
    return count;
}
```

Time complexity - O(n)

Space complexity - O(n)

 
