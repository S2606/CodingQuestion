Question:-

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

![image](https://user-images.githubusercontent.com/18497513/153030987-83edd08a-5c22-4482-972e-c7c1980650d3.png)

Example 1:

Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.

Answer:-

First observation is it should not be confused with LCA for BST, the solution is bit on a easier side for those case.

okay, in order to solve this the approach thought was that there would be two flags indicating if both elements are found or not. 
This would be followed by two traversals on both sides to check their presence and mark those flag accordingly.

Initial sol:-

```
static boolean check1;
    static boolean check2;
    
    static TreeNode LCA(TreeNode p, TreeNode q, TreeNode root){
        if(root==null){
            return null;
        }
        
        if(root.val == p.val){
            check1 = true;
            return root;
        }
        
        if(root.val == q.val){
            check2 = true;
            return root;
        }
        
        TreeNode left = LCA(p,q,root.left);
        TreeNode right = LCA(p,q,root.right);
        
        if(left!=null && right!=null){
            return root;
        }
        
        if(left==null){
            return right;
        } else {
            return left;
        }
    }
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        check1 = false;
        check2 = false;
        
        TreeNode ans = LCA(p, q, root);
        
        if(check1==true && check2==true){
            return ans;
        }
        
        return null;
    }
```

Problem with this is the cases wherein one element is parent of another is not handled properly as the other flag is never checked, hence will be returned as null.
In order to fix this, there needs to be minor tweaking of the solution as follows:-

```
static TreeNode LCA(TreeNode p, TreeNode q, TreeNode root){
        if(root==null){
            return null;
        }
        
        TreeNode temp = null;
        if(root.val == p.val){
            check1 = true;
            temp = root;
        }
        
        if(root.val == q.val){
            check2 = true;
            temp = root;
        }
        
        TreeNode left = LCA(p,q,root.left);
        TreeNode right = LCA(p,q,root.right);
        
        if(temp != null){
            return temp;
        }
        
        if(left!=null && right!=null){
            return root;
        }
        
        if(left==null){
            return right;
        } else {
            return left;
        }
    }
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        check1 = false;
        check2 = false;
        
        TreeNode ans = LCA(p, q, root);
        
        if(check1==true && check2==true){
            return ans;
        }
        
        return null;
    }
 ```
 
 - Time complexity - O(n) where n is count of all nodes
 - Space complexity - O(n) reason - the maximum element that can be in the recursion stack
