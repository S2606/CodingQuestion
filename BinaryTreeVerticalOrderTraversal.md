## The question

Given the root of a binary tree, return the vertical order traversal of its nodes' values. (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/155926765-bc73d8f0-45a3-4c0e-a027-b6093214fe3c.png)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
```

Approach:- 

![image](https://user-images.githubusercontent.com/18497513/155927883-f92a3565-fd6e-4b04-95f5-3deae25e7196.png)

If we can somehow calculatr vertical order as mentioned in the picture above, we can possibly find our answer. Also the point that needs to be considered is of
printing left to right in case of same row/column.

```
 class LevelNode {
     TreeNode node;
     int level;
     int vertical;
     
     public LevelNode(TreeNode node, int level, int vertical){
        this.node = node;
        this.level = level;
        this.vertical = vertical;
     }
 }

 public List<List<Integer>> verticalOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    
    TreeMap<Integer, ArrayList<Integer>> map = new TreeMap<>();
    
    Queue<LevelNode> queue = new LinkedList<LevelNode>();
    
    queue.add(new LevelNode(root, 0, 0));
    
    while(!queue.isEmpty()){
           LevelNode lNode = queue.poll();

          if(lNode.node!=null){
              if(!map.containsKey(lNode.vertical)){
              map.put(lNode.vertical, new ArrayList<Integer>());
              }
              map.get(lNode.vertical).add(lNode.node.val);

              if(lNode.node.left!=null){
                queue.add(new LevelNode(lNode.node.left, lNode.level+1, lNode.vertical-1));
              }

              if(lNode.node.right!=null){
                queue.add(new LevelNode(lNode.node.right, lNode.level+1, lNode.vertical+1));
              }   
          }
      }

      for(Map.Entry<Integer, ArrayList<Integer>> entry: map.entrySet()){
          result.add(entry.getValue());
      }

      return result;
 }
```

Time complexity - O(nlogn)
Space complexity - O(n)

Lets optimize this a bit further by somehow removing the sorting mechanism

```
public List<List<Integer>> verticalOrder(TreeNode root) {
      List<List<Integer>> result = new ArrayList<>();
      if (root == null) {
        return result;
      }

      HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();

      Queue<LevelNode> queue = new LinkedList<LevelNode>();

      queue.add(new LevelNode(root, 0, 0));

      int minColumn = 0, maxColumn = 0;

      while(!queue.isEmpty()){
          LevelNode lNode = queue.poll();

          if(lNode.node!=null){
              if(!map.containsKey(lNode.vertical)){
              map.put(lNode.vertical, new ArrayList<Integer>());
              }
              map.get(lNode.vertical).add(lNode.node.val);

              minColumn = Math.min(minColumn, lNode.vertical);
              maxColumn = Math.max(maxColumn, lNode.vertical);

              if(lNode.node.left!=null){
                queue.add(new LevelNode(lNode.node.left, lNode.level+1, lNode.vertical-1));
              }

              if(lNode.node.right!=null){
                queue.add(new LevelNode(lNode.node.right, lNode.level+1, lNode.vertical+1));
              }   
          }
      }

      for(int i = minColumn; i < maxColumn + 1; i++){
          result.add(map.get(i));
      }

      return result;

  }
```
Time complexity - O(n)
Space complexity - O(n)
