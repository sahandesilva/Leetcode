103. Binary Tree Zigzag Level Order Traversal

Problem:
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
```

Solution:

Time Complexity : O(n) as we should visit each node of the binary tree

Memory Complexity : O(1)


```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def zigzagLevelOrder(self, root):
        DL = []
        self.helper(root,1,DL)

        for i in range(len(DL)):
            if (i % 2) == 1:   
                DL[i].reverse()          
        return DL
         
    def helper(self,node,depthLevel,DL):
        
        if node is None:
            return
        
        if len(DL) < depthLevel:
            DL.append([])
        DL[depthLevel-1].append(node.val)

        self.helper(node.left,depthLevel+1,DL)
        self.helper(node.right,depthLevel+1,DL)       
```      

        
        
        
        
        








