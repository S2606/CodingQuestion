## The question

Given an integer n, return any array containing n unique integers such that they add up to 0.

Example 1:
```
Input: n = 5
Output: [-7,-1,1,3,4]
Explanation: These arrays also are accepted [-5,-1,1,2,3] , [-3,-1,2,-2,4].
```

Approach:- So there will be array of either even or odd length

```
if array is of length 4, the array will be[-1, -2, 1, 2]
if array is of length 5, the array will be[0, -1, -2, 1, 2]
```

okay, seems pretty straightforward from here on

```
public int[] sumZero(int n) {
  int []ans = new int[n];
  int currentAns = 1;
  int currentPointer = 0;
  
  if(n%2==1){
    ans[currentPointer++] = 0;
  }
  
  while(currentPointer<n){
      ans[currentPointer++] = currentAns;
      ans[currentPointer++] = - currentAns;
      currentAns++;
  }
  
  return ans;
}
```

Time comlexity - O(n)
Space comlexity - O(n)
