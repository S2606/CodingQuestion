### The question

You are given a 0-indexed integer array candies. Each element in the array denotes a pile of candies of size candies[i]. You can divide each pile into any number of sub piles, but you cannot merge two piles together.

You are also given an integer k. You should allocate piles of candies to k children such that each child gets the same number of candies. Each child can take at most one pile of candies and some piles of candies may go unused.

Return the maximum number of candies each child can get.

Example 1:

```
Input: candies = [5,8,6], k = 3
Output: 5
Explanation: We can divide candies[1] into 2 piles of size 5 and 3, and candies[2] into 2 piles of size 5 and 1. We now have five piles of candies of sizes 5, 5, 3, 5, and 1. We can allocate the 3 piles of size 5 to 3 children. It can be proven that each child cannot receive more than 5 candies.
```

Approach:- This is what i have tried, problem; TLE

```
public int maximumCandies(int[] candies, long k) {
        int minPile = Integer.MAX_VALUE;
        long candiesSum = 0;
        for(int candy: candies){
            minPile = Math.min(minPile, candy);
            candiesSum += candy;
        }
        
        if(candiesSum < k){
            return 0;
        }
        
        long candyPileDivided = candiesSum / k;
        long pileCount = 0;
        int maxAns = 0;
        
        while(candyPileDivided>0){
            for(int candyPile: candies){
                if((long) candyPile >= candyPileDivided){
                    pileCount += ((long) candyPile)/candyPileDivided;
                }
            }
            if(pileCount>=k){
                return (int) candyPileDivided;
            } else {
                candyPileDivided-=1;
                pileCount = 0;
            }
        }
        
        return 0;
    }
```

So now lets tweak this approach a bit by using binary search(Woah!!). 

Lets say we want to give m candies to each child from a pile candies[i]. So we need to divide at the most candies[i] / m subpiles, 
which can be added and then compared with k.

if k > sum, this means we are not providing candies to all children, which requires piles to be of smaller size(the smaller the piles, 
the greater the probability of reaching it out to all). Hence right = mid+1;

if k <= sum, this means that piles can be either greater or equal to total number of children. But since our focus is on maximizing it,
lets see if we can by keeping left = m

```
public int maximumCandies(int[] candies, long k) {
      int left = 0, right = 10_000_000;
      while(left<right){
          int mid = (left+right+1)/2;
          long sum = 0;
          for(int candy: candies){
              sum += candy/mid;
          }

          if(k>sum){
              right = mid-1;
          } else {
              left = mid;
          }
      }
      return left;
  }
```

Time complexity - O(logN)
Space complexity - O(1)
