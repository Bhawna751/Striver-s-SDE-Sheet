# Course Schedule
[Link](https://leetcode.com/problems/course-schedule/description/)

**Problem:**
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

**Approach:**
- create an adjanceny list and an indegree vector initially 0 and a queue for bfs
- if any nodes indegree is 0, push it into the queue
- while the queue is not empty:
    - pop a node, push it into the ans array
    - check the indegrees of all the neighbour nodes, decrement the indegree once
    - if anyone has indegree 0 push that node into queue
- if the size of ans is same as numCourses, return true
- else return false

Time complexity: O(V+E)
```cpp
class Solution {
public:
    bool canFinish(int V, vector<vector<int>>& prerequisites) {
        vector<int> adj[V];
        for (auto it : prerequisites) {
            adj[it[0]].push_back(it[1]);
        }
        vector<int> indegree(V, 0);
        queue<int> q;
        for (int i = 0; i < V; i++) {
            for (auto it : adj[i]) {
                indegree[it]++;
            }
        }
        vector<int> ans;
        for (int i = 0; i < V; i++) {
            if (indegree[i] == 0) {
                q.push(i);
            }
        }
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            ans.push_back(node);
            for (auto it : adj[node]) {
                indegree[it]--;
                if (indegree[it] == 0)
                    q.push(it);
            }
        }
        if(ans.size()==V)return true;
        return false;
    }
};
```
