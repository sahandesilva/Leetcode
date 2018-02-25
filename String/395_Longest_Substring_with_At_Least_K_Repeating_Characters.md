## 395. Longest Substring with At Least K Repeating Characters

### Problem:
Find the length of the longest substring T of a given string (consists of lowercase letters only) such that every character in T appears no less than k times.

Example 1:
```
Input:
s = "aaabb", k = 3

Output:
3

The longest substring is "aaa", as 'a' is repeated 3 times.
```

Example 2:
```
Input:
s = "ababbc", k = 2

Output:
5
```
The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.


### Solution:

Time complexity : O(n2)

Space Complexity: O(n)

```
class Solution(object):
    def longestSubstring(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        res = 0
        for i in range(len(s)):
            for j in range(len(s)):
                res = max(res,self.longestSubstringH(s[i:j+1], k))
        
        return res
                
    def longestSubstringH(self,s, k):
        
        D = {}
        
        for c in s:
            if not D.get(c,None):
                D[c] = 0
            D[c] += 1
        
        status = True
        
        for key in D.keys():
            if D[key] < k:
                status = False
        
        return len(s) if status else 0
```
