
# Is Graph Bipartite? (DFS)
[Link](https://leetcode.com/problems/is-graph-bipartite/description/)

**Problem:**
There is an undirected graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array graph, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

- There are no self-edges (graph[u] does not contain u).
- There are no parallel edges (graph[u] does not contain duplicate values).
- If v is in graph[u], then u is in graph[v] (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes u and v such that there is no path between them.

A graph is bipartite if the nodes can be partitioned into two independent sets A and B such that every edge in the graph connects a node in set A and a node in set B.

Return `true` if and only if it is bipartite.

**Approach:**
- Initialize a color array with all nodes initially `uncolored` represented by `-1`. `Green = 0` and `Yellow = 1`.
- Start the DFS traversal from an unvisited node and perform the following steps:
   - If a node is uncolored, color it with alternating colors.
   - If a node is previously colored, check if it follows alternate colors. If not, the graph can be said as not bipartite.
   - If all the nodes can be colored with alternating colors, the graph can be classified as bipartite.

 Time Complexity: O(V+E)
```cpp
class Solution {
public:
    bool dfs(int node, int col, vector<vector<int>> &graph, vector<int>& color){
        color[node]=col;
        for(auto it: graph[node]){
            if(color[it] == -1){
                if(!dfs(it, !col, graph, color)) return false;
            }
            else if(color[it] == col)return false;
        }
        return true;
    }
    bool isBipartite(vector<vector<int>>& graph) {
        int v = graph.size();
        vector<int> color(v,-1);
        for(int i=0;i<v;i++){
            if(color[i] == -1){
                if(!dfs(i, 0, graph, color)) return false;
            }
        }
        return true;
    }
};
```
