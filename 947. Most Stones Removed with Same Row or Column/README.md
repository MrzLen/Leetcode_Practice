### 947. Most Stones Removed with Same Row or Column

https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/description/

On a 2D plane, we place n stones at some integer coordinate points. Each coordinate point may have at most one stone.

A stone can be removed if it shares either the same row or the same column as another stone that has not been removed.

Given an array stones of length n where stones[i] = [xi, yi] represents the location of the ith stone, return the largest possible number of stones that can be removed.

```
Example 1:

Input: stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
Output: 5
Explanation: One way to remove 5 stones is as follows:
1. Remove stone [2,2] because it shares the same row as [2,1].
2. Remove stone [2,1] because it shares the same column as [0,1].
3. Remove stone [1,2] because it shares the same row as [1,0].
4. Remove stone [1,0] because it shares the same column as [0,0].
5. Remove stone [0,1] because it shares the same row as [0,0].
Stone [0,0] cannot be removed since it does not share a row/column with another stone still on the plane.
```

```
class Solution:
    def removeStones(self, stones: List[List[int]]) -> int:
        rows=defaultdict(list)
        
        cols=defaultdict(list)
        
        for l,k in enumerate(stones):
            rows[k[0]].append(l)
            cols[k[1]].append(l)
            
        n = len(stones)
        vis = [False]*n
        
        
        def dfs(node,vis):
            ans[0] += 1
            vis[node] = True
            for i in rows[stones[node][0]]:
                if vis[i] == False:
                    dfs(i,vis)
            for i in cols[stones[node][1]]:
                if vis[i] == False:
                    dfs(i,vis)
        ans_ = 0

        for i in range(0,n):
            if vis[i] == False:
                ans = [0]
                dfs(i,vis)
                ans_ += ans[0]-1
        return ans_
```
