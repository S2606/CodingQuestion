## The question

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/155750129-f62002f3-a9c8-4de9-b7cb-d979d74572bb.png)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

Approach:- Intially O(n^2) approach did cross my mind. But i guess this can be solved with bit greedy method. How? so we need to find poles of greate height, right?
Can have two pointers on both end, the positions can be changed based on height checks. Solution can be made on O(n)

```
public int maxArea(int[] height) {
  int maxarea = 0, l = 0, r=height.length-1;
  while(l<r){
      maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r-l));
      if(height[l]<height[r]){
          l++;
      } else {
          r--;
      }
  }
  
  return maxarea;
}
```

Time complexity - O(n)
Space complexity - O(n)
