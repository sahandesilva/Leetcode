
Problem:
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.
```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```


Solution : Bruteforce - Recursive
```
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) < 3:
            return []
        
        ansB = []
        runningsum = []
        self.threeSumH(nums,ansB,runningsum,0)
        return ansB
        
    def threeSumH(self, nums,ansB,runningsum,index):
        
        if len(runningsum) == 3:
            if sum(runningsum) == 0:
                t = sorted(runningsum[:])
                if  t not in ansB:
                    ansB.append(t[:])
            return
     
        for i in range(index,len(nums)):
            runningsum.append(nums[i])
            self.threeSumH(nums,ansB,runningsum,i + 1)
            runningsum.pop()    

```




Solution: Using two pointers - Iterative
```
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        ansB = []   
        nums.sort()
        
        for i in range(len(nums) - 2):
            if i > 0 and nums[i] == nums[i-1]:
                continue
                
            sum1 = nums[i]
            lo,hi = i+1,len(nums) -1

            while lo < hi:
                if (sum1 + nums[lo] + nums[hi]) == 0:
                    ansB.append([sum1,nums[lo],nums[hi]])
                    while lo < hi and nums[lo] == nums[lo + 1]: lo += 1 
                    while lo < hi and nums[hi] == nums[hi - 1]: hi -= 1 

                    lo += 1
                    hi -= 1
                elif (sum1 + nums[lo] + nums[hi])  > 0:
                    hi -= 1   
                else:
                    lo += 1
                
                    
        return ansB 
        ```
