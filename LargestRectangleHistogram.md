## The question

## Asked in Groww 2021

Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/155284048-215bbde0-4d89-441e-8b9c-55d1cf9df711.png)

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

Initial approach:- have two for loops, one which will be treated as starting point, next for finding blocks which can contribute towards creating a alrger histogram
by area. Time complexity - O(n^2)

Now we know this can be optimized. But how? Divide and conquer (this will give time complexity of O(nlogn))? 
Can be optimized bit further by using stacks and being greedy!

```
elements in stack are represented as height(index)

Dry run:-
[2,1,5,6,2,3]
stk = [-1]

ele= 2
stk=[-1, 2(0)]
area = 2

ele= 1
stk= [-1, 1(1)]  // 2 was removed because it did not make any sense to create a larger histogrsm with block of smaller size(this would minimize the area, not the other way around)
area= (i-stk[top-1]-1)*height[stk[top]] = (1-(-1)-1)*2 = 2

ele= 5
stk= [-1, 1(1), 5(2)] // maybe 5 could help in creating larger histogram owing to larger size
area = 2

ele= 6
stk= [-1,1(1), 5(2), 6(3)] // maybe 6 could help in creating larger histogram owing to larger size
area = 2

ele= 2
stk=[-1, 1(1), 5(2)]
area = (i-stk[top-1]-1)*height[stk[top]] = (4-2-1)*6 = 6
stk=[-1, 1(1)]
area = (i-stk[top-1]-1)*height[stk[top]] = (4-1-1)*5 = 10

ele = 3
stk=[-1, 1(1), 3(4)]
```

Code:-
```
public int largestRectangleArea(int[] heights) {
  Stack<Integer> stk = new Stack<Integer>();
  stk.push(-1);
  int maxArea = 0;
  for(int i=0;i<heights.length();i++){
       while(stk.size()>1 && heights[stk.peek()] > heights[i]){
          int ele = stk.pop();
          maxArea = Math.max(maxArea, (i-stk.peek()-1)*height[ele]);
       }
       
       stk.push(i); 
  }
  
  while(stk.size()!=1){
      int ele = stk.pop();
      maxArea = Math.max(maxArea, (heights.length-stk.peek()-1)*height[ele]);
  }
  
  return maxArea;
        
}
```

Time complexity - O(n)

Space complexity - O(n)

