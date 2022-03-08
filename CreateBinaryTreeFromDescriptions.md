## The question

You are given a 2D integer array descriptions where descriptions[i] = [parenti, childi, isLefti] indicates that parenti is the parent of childi in a binary tree of unique values. Furthermore,

    If isLefti == 1, then childi is the left child of parenti.
    If isLefti == 0, then childi is the right child of parenti.

Construct the binary tree described by descriptions and return its root.

The test cases will be generated such that the binary tree is valid.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/157148144-5e10fe13-d716-47b6-b8b3-c7c8d9a83d4d.png)

```
Input: descriptions = [[20,15,1],[20,17,0],[50,20,1],[50,80,0],[80,19,1]]
Output: [50,20,80,15,17,19]
Explanation: The root node is the node with value 50 since it has no parent.
The resulting binary tree is shown in the diagram.
```

Approach:- Access of elements needs to be faster for creation of tree, along with simple framework for creation of binary tree. Can use HashMap for first usecase. 
Also can store children in a set such that the root can almost never-ever be a child right?

```
public TreeNode createBinaryTree(int[][] descriptions) {
      HashMap<Integer, TreeNode> map = new HashMap<Integer, TreeNode>();
      Set<Integer> children = new HashSet<>();
      int root = -1;
      for(int [] description: descriptions){
          int parent = description[0];
          int child = description[1];
          int isLeft = description[2];

          children.add(child);
          TreeNode node = map.getOrDefault(parent, new TreeNode(parent));
          if(isLeft==1){
              node.left = map.getOrDefault(child, new TreeNode(child));
              map.put(child, node.left);
          } else {
              node.right = map.getOrDefault(child, new TreeNode(child));
              map.put(child, node.right);
          }

          map.put(parent, node);
      }

      for(int [] description: descriptions){
          if(!children.contains(description[0])){
              root = description[0];
              break;
          }
      }

      return map.getOrDefault(root, null);
  }
```

Time complexity - O(n)
Space complexity - O(n)
