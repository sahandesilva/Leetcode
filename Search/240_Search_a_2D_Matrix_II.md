## 240. Search a 2D Matrix II

**Problem :**

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.
For example,

Consider the following matrix:
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Given target = 5, return true.

Given target = 20, return false.

### Solution:

Time Complexity is O(nlogn) and Space Complexity is O(1)

```
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        for i in range(len(matrix)):
            if self.searchMatrixH(matrix, target,i,0,len(matrix[0])-1):
                return True
        
        return False
    
    
    def searchMatrixH(self, matrix, target,row,start,end):
        
        if start > end:
            return False
        
        mid = (start + end) // 2
        
        if matrix[row][mid] == target:
            return True
        elif matrix[row][mid] > target:
            return self.searchMatrixH(matrix, target,row,start,mid-1)
        else:
            return self.searchMatrixH(matrix, target,row,mid+1,end)
```
