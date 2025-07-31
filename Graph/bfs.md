# Breadth First Search

Given an undirected connected graph with `V` vertices numbered from 0 to V-1, the task is to implement Breadth First Search (BFS) traversal starting from the 0th vertex.

**Approach:**
- Mark all nodes as unvisited. Create an empty queue.
- Enqueue the source node. Mark the source node as visited.
- While the queue is not empty:
    - Dequeue the front node. Process the node.
    - For each adjacent unvisited node, enqueue the adjacent node and mark it as visited.    
    - Repeat the process until all nodes are visited.
Time Complexity: O(V+E)

Code:
```cpp
vector<int> bfsOfGraph(int V, vector<int> adj[]) {
        int vis[V]={0};
        vis[0]=1;
        queue<int> q;
        q.push(0);
        vector<int> bfs;
        while(!q.empty()){
            int node = q.front();
            q.pop();
            bfs.push_back(node);

            for(auto it:adj[node]){
                if(!vis[it]){
                    vis[it]=1;
                    q.push(it);
                }
            }
        }
        return bfs;
}
```
