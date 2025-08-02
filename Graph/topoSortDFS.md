# Topological sort  (DFS)

**Problem:** Given a Directed Acyclic Graph (DAG) with V vertices labeled from 0 to V-1.The graph is represented using an adjacency list where adj[i] lists all nodes connected to node. Find any Topological Sorting of that Graph.

In topological sorting, node u will always appear before node v if there is a directed edge from node u towards node v(u -> v).

The Output will be True if your topological sort is correct otherwise it will be False.

**Approach:**
1. traverse all components of the graph.
2. carry a visited array and a stack, where we are going to store the nodes after completing the DFS call.
3. In the DFS call, first, the current node is marked as visited. Then DFS call is made for all its adjacent nodes.
4. After visiting all its adjacent nodes, DFS will backtrack to the previous node and meanwhile, the current node is pushed into the stack.
5. Finally, we will get the stack containing one of the topological sortings of the graph.

Time Complexity: O(V+E)+O(V)

Space Complexity: O(2N) + O(N) ~ O(2N)

```cpp
class Solution{
public:
    void dfs(int node, vector<int> adj[],vector<int> &vis, stack<int>&st){
        vis[node]=1;
        for(auto it: adj[node]){
            if(vis[it]==0) dfs(it, adj, vis, st);
        }
        st.push(node);
    }
    vector<int> topoSort(int V, vector<int> adj[]){
        vector<int> ans;
        stack<int> st;
        vector<int> vis(V,0);
        for(int i=0;i<V;i++){
            if(!vis[i]){
                dfs(i, adj, vis, st);
            }
        }
        while(!st.empty()){
            ans.push_back(st.top());
            st.pop();
        }
        return ans;
    }
};
```

