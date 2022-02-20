## The question

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

Example 1:

Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Initial approach:- Sort the array, and then check it in another pass. Time complexity O(nlogn)

So can we optimize this? Yes. How? So why were we sorting in first place? To improve access of consecutive elements right. Can also be done with HashSets in O(1).
All we need to do is generate sequence and check elements

```
public int longestConsecutive(int[] nums) {
        HashSet<Integer> set = new HashSet<Integer>();
        for(int num: nums){
            set.add(num);
        }
        
        int longestSeq = 0;
        
        for(int num: set){
          if(!set.contains(num-1)){
             // To check if previous element exists, thereby reducing chance of finding sequence of small size
             int currNum = num;
             int currentSeq = 1;
             
             while(set.contains(currNum+1)){
                   currNum += 1;
                   currentSeq += 1;
             }
             
             longestSeq = MAth.max(currentSeq, longestSeq);
          }
        }
        
        return longestSeq;
}
```

Time complexity - O(N) WHAAATTT!! Shocked right? If you look closely, the inner while loop runs at max n times, thereby total time complexity is not O(n*n) but instead O(n+n)

Space complexity - O(N)
