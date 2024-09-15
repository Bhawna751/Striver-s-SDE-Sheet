## Depth First Search (DFS)
Given an undirected graph, return a vector of all nodes by traversing the graph using depth-first search (DFS).

Example 1:

Input:


<img src = "https://lh6.googleusercontent.com/yQxrjm3_PAP7YbKRwtyz14xWvOQEFLMsLUarnZFSEm4qpB4gKR4NhlKTsNcF_WUkC2TQWOoT9A75KWG7ISIS5Ger-sCq5enP7vtQPxPJaUDh_3XCb_InMc7dAqWXBtm_-kUNBpN80LnSe7Glirts9TA" 
    height=200px width=350px />

Output: 1 2 3 4 5 6 7 8 9 10

**Approach:**
- recursion and backtracking , goes in-depth, i.e., traverses all nodes by going ahead, and when there are no further nodes to traverse in the current path, then it backtracks on the same path and traverses
other unvisited nodes.
- start with a node `v`, mark it as `visited` and store it in the solution `vector`. It is unexplored as its adjacent nodes are not visited.
- run through all the adjacent nodes, and call the recursive dfs function to explore the node `v` which has not been visited previously. This leads to the exploration of another node `u` which is its adjacent
node and is not visited. 
- adjacency list stores the list of neighbours for any node. Pick the neighbour list of node `v` and run a for loop on the list of neighbours , go in-depth with each node. When node `u` is explored completely
then it backtracks and explores node `w`.
- terminate when all the nodes are completely explored.

```cpp
class Solution {
  private: 
    void dfs(int node, vector<int> adj[], int vis[], vector<int> &ls) {
        vis[node] = 1; 
        ls.push_back(node); 
        // traverse all its neighbours
        for(auto it : adj[node]) {
            // if the neighbour is not visited
            if(!vis[it]) {
                dfs(it, adj, vis, ls); 
            }
        }
    }
  public:
    // Function to return a list containing the DFS traversal of the graph.
    vector<int> dfsOfGraph(int V, vector<int> adj[]) {
        int vis[V] = {0}; 
        int start = 0;
        // create a list to store dfs
        vector<int> ls; 
        // call dfs for starting node
        dfs(start, adj, vis, ls); 
        return ls; 
    }
};
```
