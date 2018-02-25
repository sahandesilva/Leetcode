## 238. Product of Array Except Self

### Problem:

</br>

Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].

Follow up:
Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)
</br>
</br>

### Solution:
Time complexity: O(n)

Memory Complexity: O(1)
</br>


```
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        output = [1 for i in range(len(nums))]
        runningSum = nums[0]
        length = len(nums)
        
        for i in range(1,length):
            output[i] = runningSum
            runningSum *= nums[i] 
        
        runningSum = 1
        for i in range(length):
            output[length - 1 - i] *= runningSum
            runningSum *= nums[length - 1 - i]
                      
        return output
 ```       
