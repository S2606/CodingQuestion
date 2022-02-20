## The question

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/154847111-3d076d2e-e084-46bb-9fdf-31cf5651a77b.png)

Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

Initial approach:- If the are m nodes in a tree, it will take O(m^2) [time complexity](https://stackoverflow.com/questions/32090702/finding-all-longest-unique-paths-in-tree). Can we optimize this?
Lets think...  What is path sum?

- A path sum is basically sum of:-
  - parent and left child or
  - parent and right child or
  - parent and both children
- If you notice the first two points, the only thing that is crossing my skull is that can it be solved by recursion?

- If we consider recursion, lets go step-by-step
  - Does it have optimal substructure property?
    - Yes, The lower the tree, the further its chances of joiningin the sum
      - Sum(i) = Math.max(i, Sum(i.left) + i, Sum(i.right) + i, Sum(i.left) + Sum(i.right) + i);
        Where i is the node of a tree.
  - Does it have overlapping subproblem property?
    - No, because in trees if a node is used once, it will not bw used again. There are independent subsets in trees related recursion if you think.
- Okay, since we have found an optimal substructure, can we now write some pseudo-code?

```
int totalSum = 0;

public int maxPathSum(TreeNode root) {
     if(root==null){
          return 0;
     }
     
     int leftSum = maxPathSum(root.left);
     int rightSum = maxPathSum(root.right);
     
     int maxSingle = Math.max(Math.max(leftSum, rightSum)+root.val, root.val);
     int maxTotal = Math.max(maxSingle, leftSum + rightSum + root.val);
     totalSum = Math.max(totalSum, maxTotal);
     return maxSingle;
}
```
Time complexity - O(m) where m is number of elements
Space complexity - O(H) where H is tree height = O(log m)
