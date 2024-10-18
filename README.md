# Path Sum III

## https://leetcode.com/problems/path-sum-iii

Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values along the path equals targetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

![Path Sum III](example.JPG?raw=true)


# Implementation 1a : O(n^2)
```java
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

## Implementation 1b : O(n^2) Making leetcode happy (when node.val is very large, target-node.val can lead to integer overflow)
```java
class Solution {
   public int pathSum(TreeNode root, int sum) {
        if(root == null)
            return 0;
        return pathSum(root.left, sum) + pathSum(root.right, sum) + findPath(root, sum);
   }

    public int findPath(TreeNode node, long target){
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

# Implementation 2 : O(n) Using Prefix Sum
```java
class Solution {
    public int pathSum(TreeNode root, int targetSum) {
        Map<Long, Integer> map = new HashMap<>();
        map.put(0L, 1);
        return helper(root, (long) targetSum, 0, map);
    }

    private int helper(TreeNode node, long targetSum, long prefixSum, Map<Long, Integer> map) {
        if (node == null) {
            return 0;
        }
        prefixSum += node.val;
        int count = map.getOrDefault(prefixSum - targetSum, 0);
        map.put(prefixSum, map.getOrDefault(prefixSum, 0) + 1);
        count += helper(node.left, targetSum, prefixSum, map) + helper(node.right, targetSum, prefixSum, map);
        map.put(prefixSum, map.get(prefixSum) - 1);
        return count;
    }
}
```


# References :
1. https://www.youtube.com/watch?v=uZzvivFkgtM
2. https://github.com/ojasmaru/LetsAlgoTogether/blob/master/Path%20Sum%20III/Java/QuickStart.java


