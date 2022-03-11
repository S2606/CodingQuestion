## The question

Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values along the path equals targetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

Example 1:

![image](https://user-images.githubusercontent.com/18497513/157485847-86049891-f48a-4273-92e6-58ecd6f901a0.png)

```
Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.
```

Approach:- Seems like pre-order tree traversal of tree will help here, along with storage of count as global variable, point to be considered is that root elements can be ignored

So sum can be found in two ways:- one by traversing to that sum, other by getting k-sum (#Prefix Sum). Both of these can be stored and fetched via an HashMap.

```
int k;
int count = 0;
HashMap<Integer, Integer> map = new HashMap<>();

public void preorder(TreeNode root, int currSum){
  if(root==null){
    return;
  }
  
  currSum += root.val;
  
  if(currSum==k){
    count+=1;
  }
  
  count += map.getOrDefault(currSum-k, 0);
  
  map.put(currSum, map.getOrDefault(currSum, 0)+1);
  
  preorder(root.left, currSum);
  preorder(root.right, currSum);
  
  map.put(currSum, map.getOrDefault(currSum, 0)-1);
}

public int pathSum(TreeNode root, int targetSum) {
    k = targetSum;
    preorder(root, 0);
    return count;
}
```

Time complexity - O(N)

Space complexity - O(N)
