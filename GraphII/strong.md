# KosaRaju algo

**Problem:**
Given a Directed Graph with V vertices (Numbered from 0 to V-1) and E edges. An edge is represented [ai,bi] denoting a directed edge from vertex ai to bi. Find the number of strongly connected components in the graph.

Kosaraju's Algorithm:

- **Sort all the nodes according to their finishing time:** Perform a DFS call to sort the nodes based on their finishing time and store them in a stack.
- **Reverse all the edges of the entire graph:**
  - Create a new graph where all the edges of the original graph will be reversed.
- **Perform the DFS and count the number of different DFS calls to get the number of SCC:**
  - Start DFS traversal on the reversed graph from the node which is on the top of the stack and continue until the stack becomes empty.
  - For each DFS call, the counter representing the number of SCCs can be incremented by 1.
    
**Approach:**
- Create a visited array and a stack to store nodes based on their finishing times during DFS traversal.
- Perform a DFS on the original graph to determine the finishing times of nodes.
- Each node is pushed onto the stack after all its descendants are processed.
- Reverse the edges of the original graph to create a transposed graph. Perform DFS on the transposed graph, starting from the nodes in the order defined by the stack 
- Count the number of DFS trees formed in this step
- return count

```cpp
class Solution{
public:
    void dfs(int node, vector<int>&vis, vector<int> adj[], stack<int>&st){
        vis[node]=1;// 1 1 1 0 0 0 0 0 
        for(auto it:adj[node]){
            if(!vis[it]){
                dfs(it, vis, adj, st);
            }
        }//st-> 2 1 0
        st.push(node);
    }
    void helper(int node, vector<int>&vis, vector<int> transpose[]){
        vis[node]=1;
        for(auto it : transpose[node]){
            if(!vis[it]) helper(it, vis, transpose);
        }
    }
    int kosaraju(int V, vector<int> adj[]){
      vector<int> vis(V,0);
      stack<int> st;
      for(int i=0;i<V;i++){
        if(!vis[i]){
            dfs(i,vis,adj,st);
        }
      }
      vector<int> transpose[V];
      for(int i=0;i<V;i++){
        vis[i]=0;
        for(auto it:adj[i]){
            transpose[it].push_back(i);
        }
      }
      int cnt=0;
      while(!st.empty()){
        int node = st.top();
        st.pop();
        if(!vis[node]){
            cnt++;
            helper(node,vis,transpose);
        }
      }
      return cnt;
    }
};
```
