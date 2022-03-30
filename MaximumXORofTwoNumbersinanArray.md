### The question

Given an integer array nums, return the maximum result of nums[i] XOR nums[j], where 0 <= i <= j < n.

Example 1:

```
Input: nums = [3,10,5,25,2,8]
Output: 28
Explanation: The maximum result is 5 XOR 25 = 28.
```

Approach:-

![Screenshot 2022-03-30 at 10 20 29 PM](https://user-images.githubusercontent.com/18497513/160889014-3b1d8191-7cec-4fea-9655-f1076752899d.png)

Lets Code
```
public int findMaximumXOR(int[] nums) {
    int maxNo = nums[0];
    for(int num: nums) maxNo = Math.max(maxNo, num);
    int L = (Integer.toBinaryString(maxNo)).length();
    
    int maxXOR = 0, currXOR;
    Set<Integer> prefixes = new HashSet<Integer>();
    for(int i=L-1; i>-1; i--){
      maxXOR <<= 1;
      currXOR = maxXOR | 1;
      prefixes.clear();
      for(int num: nums) prefixes.add(num>>i);
      for(int prefix: prefixes){
          if(prefixes.contains(prefix^currXOR)){
             maxXOR = Math.max(maxXOR, currXOR);
             break;
          }
      }
    }
    
    return maxXOR;
}
```

Time complexity - O(N) where N is for first loop, 2^L-i * 2^L-i for second loop. Sum it and one will find the answer.
Space complexity - O(1)
