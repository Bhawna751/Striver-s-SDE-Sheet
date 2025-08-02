# Topological sort or Kahn's algorithm (BFS)

**Problem:** Given a Directed Acyclic Graph (DAG) with V vertices labeled from 0 to V-1.The graph is represented using an adjacency list where adj[i] lists all nodes connected to node. Find any Topological Sorting of that Graph.

In topological sorting, node u will always appear before node v if there is a directed edge from node u towards node v(u -> v).

The Output will be True if your topological sort is correct otherwise it will be False.

**Approach:** 
1. calculate the indegree of each node and store it in the indegree array. iterate through the given adj list, and simply for every node u->v, we can increase the indegree of v by 1 in the indegree array. 
2. push the node(s) with indegree 0 into the queue.
3. pop a node from the queue including the node in our answer array, and for all its adjacent nodes, we will decrease the indegree of that node by one
4. After that, if for any node the indegree becomes 0, we will push that node again into the queue.
5. repeat steps 3 and 4 until the queue is completely empty. 

Time Complexity: O(V+E)

```cpp
class Solution{
public:
    vector<int> topoSort(int V, vector<int> adj[]){
        vector<int> indegree(V,0);
        queue<int> q;
        vector<int> ans;
        for(int i=0;i<V;i++){
            for(auto it: adj[i]) indegree[it]++;
        }
        for(int i=0;i<V;i++){
            if(indegree[i]==0)q.push(i);
        }
        while(!q.empty()){
            int node=q.front();
            q.pop();
            ans.push_back(node);
            for(auto it:adj[node]){
                indegree[it]--;
                if(indegree[it]==0)q.push(it);
            }
        }
        return ans;
    }
};

```
