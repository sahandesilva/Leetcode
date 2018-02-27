## 684. Redundant Connection

### Problem:

In this problem, a tree is an undirected graph that is connected and has no cycles.

The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.

The resulting graph is given as a 2D-array of edges. Each element of edges is a pair [u, v] with u < v, that represents an undirected edge connecting nodes u and v.

Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge [u, v] should be in the same format, with u < v.

Example 1:

```
Input: [[1,2], [1,3], [2,3]]
Output: [2,3]
Explanation: The given undirected graph will be like this:
  1
 / \
2 - 3
```

Example 2:

```
Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
Output: [1,4]
Explanation: The given undirected graph will be like this:
5 - 1 - 2
    |   |
    4 - 3
```
Note:
The size of the input 2D-array will be between 3 and 1000.
Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.

Update (2017-09-26):
We have overhauled the problem description + test cases and specified clearly the graph is an undirected graph. For the directed graph follow up please see Redundant Connection II). We apologize for any inconvenience caused.

### Solution 1:
**Using Union Find without union by rank**

Time Complexit : O(N)

Memory Complexity : O(N)

```
class Solution(object):
    def findRedundantConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """ 
        
        parent = [i for i in range(len(edges)+1)]
        
        def merge(u,parentU):
            for i in range(len(parent)):
                if parent[i] == u:
                    parent[i] = parentU

        for u,v in edges:
            if parent[u] == parent[v]:
                return (u,v)
            
            if v == parent[v]:
                parent[v] = parent[u]
                merge(v,parent[v])
            elif u == parent[u] :
                parent[u] = parent[v]  
                merge(u,parent[u])
            else:
                t = parent[u]
                parent[u] = parent[v]      
                merge(t,parent[u])
```                
### Soluton 2:
**Using UnionFind with union-by-rank**

```
class Solution(object):
    def findRedundantConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """ 
        uf = UnionFind(edges)
        
        for edge in edges:
            if not uf.union(*edge):
                return edge
        
class UnionFind(object):
    def __init__(self,edges):
        self.parent = [i for i in range(len(edges)+1)]
        self.rank = [0]*(len(edges)+1)
            
    def find(self,node):
        
        if self.parent[node] != node:    
            self.parent[node] = self.find(self.parent[node])        
        return self.parent[node]

    def union(self,u,v):
        
        pu,pv = self.find(u),self.find(v)
        
        if pu == pv:
            return False
        elif self.rank[pu] > self.rank[pv]:
            self.parent[pv] = pu
        elif self.rank[pv] > self.rank[pu]:
            self.parent[pu] = pv
        else:
            self.parent[pv] = pu
            self.rank[pu] += 1
            
        return True
 ```          
      
    
    
        
            
        
        
        
        
        
        
        
        
        
        
        
            
            
        
        
        
        
            
        
        

