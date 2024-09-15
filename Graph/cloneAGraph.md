## [133. Clone Graph](https://leetcode.com/problems/clone-graph/description/)
Given a reference of a `node` in a connected undirected graph.

Return a deep copy (clone) of the graph.

Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.
```
class Node {
    public int val;
    public List<Node> neighbors;
}
```
Test case format:
- For simplicity, each node's value is the same as the node's index (1-indexed). For example, the first node with val == 1, the second node with val == 2, and so on. The graph is represented in the test case
  using an adjacency list.
- An adjacency list is a collection of unordered lists used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.
- The given node will always be the first node with val = 1. You must return the copy of the given node as a reference to the cloned graph.

Example 1:


<img src= "https://assets.leetcode.com/uploads/2019/11/04/133_clone_graph_question.png" style="height: 400px; width:400px;"/>


```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
```

Explanation: There are 4 nodes in the graph.
- 1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
- 2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
- 3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
- 4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).

**Algorithm:**
- Traverse all nodes of original graph and as soon as we reach a node, we will make a copy node. And recur for rest of the graph.
- This is a typical recursion type problem implemented on Graph.
- For 'Recursion' we use basically `DFS` or `BFS`. I am using **DFS**

1. We use HashMap to solve it and using DFS.
2. Initially our hash map will be empty and we try to map the old node with the new node or the copy node.
3. We start with any entry point.
4. I am using '1' as my entry point.

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    Node* dfs(Node* node, unordered_map<Node*, Node*>&mpp){
        vector<Node*> neighbor;
        Node* clone = new Node(node->val);
        mpp[node] = clone;
        for(auto it: node->neighbors){
            if(mpp.find(it) != mpp.end()) neighbor.push_back(mpp[it]);
            else neighbor.push_back(dfs(it,mpp));
        }
        clone -> neighbors = neighbor;
        return clone;
    }
    Node* cloneGraph(Node* node) {
        unordered_map<Node*,Node*> mpp;
        if(node == NULL) return NULL;
        if(node->neighbors.size() == 0){
            Node* clone = new Node(node->val);
            return clone;
        }
        return dfs(node,mpp);
    }
};
```
