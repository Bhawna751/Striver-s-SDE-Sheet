# Course Schedule

**Problem:**
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i]` = `[ai, bi]` indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

**Approach: (DFS)**
- create an adjacency list and visited array
- call the dfs function to check for a cycle:
    - if the node is already visited (vis[node]==1) return true;
    - if the node is not already visited (vis[node]==0) :
        - mark it as visited
        - check if the neighbours have a cycle and return true
    - if no cycle was found via this cur node then mark vis[node]=2
    - and return false
- if dfs  function return true then return false;
- else default case is return true
Time Complexity: O(N+2E) + O(N)

 ```cpp
class Solution {
public:
    bool cycle(vector<int> adj[], vector<int> &vis, int node){
        if(vis[node]==1)return true;
        if(vis[node]==0){
            vis[node]=1;
            for(auto it: adj[node]){
                if(cycle(adj, vis, it)) return true;
            }
        }
        vis[node]=2;
        return false;
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> adj[numCourses];
        for(auto it: prerequisites){
            adj[it[1]].push_back(it[0]);
        }
        vector<int> vis(numCourses,0);
        for(int i=0;i<numCourses;i++){
            if(cycle(adj, vis, i)) return false;
        }
        return true;
    }
};
```
