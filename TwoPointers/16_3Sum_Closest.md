
## 16. 3Sum Closest

### Problem:
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
   
   </br> 
   </br> 
   
### Solution:

Time Complexity: O(n2) - Average Case and Worst Case
Space Complexity : O(1)
</br>
</br>

```
import sys
class Solution(object):
    def threeSumClosest(self, nums,target):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = sys.maxsize
        nums.sort()
        
        for i in range(len(nums)-1):
            lo = i + 1
            hi = len(nums)-1

            while lo < hi:
                ans = nums[i] + nums[lo] + nums[hi]
                
                if abs(ans - target) < abs(res-target):
                    res = ans       
                if ans <  target:
                    lo += 1
                elif ans >  target:
                    hi -= 1
                else:
                    return res
        return res
```
