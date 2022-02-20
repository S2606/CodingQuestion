## The question

### P.S.:- this was asked in Flipkart 2021

Nearly everyone has used the Multiplication Table. The multiplication table of size m x n is an integer matrix mat where mat[i][j] == i * j (1-indexed).

Given three integers m, n, and k, return the kth smallest element in the m x n multiplication table.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/154849001-427f4743-ae36-4c12-9e60-670b2224601c.png)

Input: m = 3, n = 3, k = 5
Output: 3
Explanation: The 5th smallest number is 3.

- Initial approach:- Push all elements in an array, sort them and find the smallest element. Time complexity - O(mn log(mn)). Can this be optimized?

- Another approach:- Have three pointers which are pointed to first element of each row, push them into a priorityqueue for sorting, move the pointer which has the 
smallest element, move them to next element till count == kth smallest element. Time complexity O(k * mlogm)=O(m^2n logm). 
This was the final answer given to the interviewer.

### Big mistake was not considering binary search at all!!

### If your input size is quite big, consider logarithmic solutions

- So can binary search be used here?? YES, how? the count factor can be checked is that till a particular element, if we can somehow know that 
there are k elements smaller than that element, can we safely say that that element is a candidate for our answer?? YES, if this 
clear how will the count procedure take place?? So in order to count smaller elements, remembering the point that numbers are represented in [i, 2*i, 3*i,..] 
fashion, then they should be calculated as x//i. Okay so with jargons aside, lets see the code

```
public bool enough(int mi, int m, int n, int k){
  int count = 0;
  for(int i=1;i<=m;i++){
    count += Math.min(x/i, n);
  }
  return count >= k;
}

public int findKthNumber(int m, int n, int k) {
  int lo = 1, hi = m * n;
  while(lo < hi){
      int mi = lo + (hi-lo)/2;
      if(!enough(mi, m, n, k)) low = mi+1;
      hi = mi;
  }
  
  return lo;
}
```
Time complexity - O(m*logmn)
Space complexity - O(1)
