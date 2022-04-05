### The question

You are given an integer array bloomDay, an integer m and an integer k.

You want to make m bouquets. To make a bouquet, you need to use k adjacent flowers from the garden.

The garden consists of n flowers, the ith flower will bloom in the bloomDay[i] and then can be used in exactly one bouquet.

Return the minimum number of days you need to wait to be able to make m bouquets from the garden. If it is impossible to make m bouquets return -1.

Example 1:

```
Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3
Explanation: Let us see what happened in the first three days. x means flower bloomed and _ means flower did not bloom in the garden.
We need 3 bouquets each should contain 1 flower.
After day 1: [x, _, _, _, _]   // we can only make one bouquet.
After day 2: [x, _, _, _, x]   // we can only make two bouquets.
After day 3: [x, _, x, _, x]   // we can make 3 bouquets. The answer is 3.
```

Approach:-

![Screenshot 2022-04-05 at 10 14 07 PM](https://user-images.githubusercontent.com/18497513/161804585-56f51b1d-e246-486a-b9c1-7638be50bf9f.png)

Lets code:-

```
public int minDays(int[] A, int m, int k) {
        int n = A.length, left = 1, right = (int)1e9;
        if(m*k > n) return -1;
        while(left<right){
            int mid = (left + right)/2, flow = 0, bouq = 0;
            for(int i=0;i<n;i++){
                if(A[i]>mid){
                    flow = 0;
                } else if(++flow>=k){
                    bouq++;
                    flow = 0;
                }
            }
            
            if(bouq < m){
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return left;
    }
```

Time complexity - O(Nlog(maxA)) Note that the result must be one A[i], so actually we can sort A in O(NlogK), Where K is the number of different values.
and then binary search the index of different values.
Space complexity - O(1)
