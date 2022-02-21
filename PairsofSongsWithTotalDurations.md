## The question

You are given a list of songs where the ith song has a duration of time[i] seconds.

Return the number of pairs of songs for which their total duration in seconds is divisible by 60. Formally, we want the number of indices i, j such that i < j with (time[i] + time[j]) % 60 == 0.

Example 1:

```
Input: time = [30,20,150,100,40]
Output: 3
Explanation: Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
```

Initial Approach:- Find all pairs, complexity O(n^2). Can this be optimized?

Yes, but for that, we need to see some math

```
Assuming time[i] is x, time[j] is y
(x+y)%60 = 0
((x%60)+(y%60))%60 = 60 % 60
(x%60)+(y%60) = 60
x%60 = 60-y%60
```

- Now since the math is clear, all we need to do is know y, find x, store it in a data structure with time complexity of access as O(1) 
or can use fixed int size because no nummber will be greater than 60 and voila!

```
 public int numPairsDivisibleBy60(int[] time) {
      int remainder[] = new int[60];
      int count=0;
      for(int t: time){
          if(t%60==0){
              count += remainder[t%60];
          } else {
              count += remainder[60 - t%60];
          }
          remainder[t%60]++;
      }
      return count;
 }
 ```
 
 Time complexity = O(n) Space complexity O(1)
