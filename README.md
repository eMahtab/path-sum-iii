# Path Sum III

## https://leetcode.com/problems/path-sum-iii

Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values along the path equals targetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

![Path Sum III](example.JPG?raw=true)


# Implementation : O(n^2)
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
   public int pathSum(TreeNode root, int sum) {
        if(root == null)
            return 0;
        return pathSum(root.left, sum) + pathSum(root.right, sum) + findPath(root, sum);
   }

    public int findPath(TreeNode node, int target){
        int numberOfPathFound = 0;
        if(node.val == target)
            numberOfPathFound++;
        if(node.left != null)
            numberOfPathFound += findPath(node.left, target - node.val);
        if(node.right != null)    
            numberOfPathFound += findPath(node.right, target - node.val);
        
        return numberOfPathFound;
    }
}
```


# References :
1. https://www.youtube.com/watch?v=uZzvivFkgtM



