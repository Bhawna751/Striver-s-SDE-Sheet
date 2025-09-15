### Level Order Traversal

**Problem:** Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

**Approach:**
- initialize an empty queue to hold nodes as we traverse the tree level by level.
- Enqueue the root node into the queue. If the tree is empty, return an empty 2D vector immediately.
- While the queue is not empty, process each level of the tree:
    - Determine the number of nodes at the current level by checking the size of the queue.
    - Create a temporary vector to store the values of nodes at this level.
    - For each node at the current level:
        - Dequeue the front node from the queue.
        - Store the node’s value in the temporary vector.
        - Enqueue the left and right children of the current node (if they exist) into the queue.
    - After processing all nodes at the current level, add the temporary vector to the final 2D vector representing the level order traversal.
- Once all levels are processed, return the 2D vector containing the level-order traversal of the binary tree.

**Code:** 
```cpp
class Solution {
public:
    vector<vector<int> > levelOrder(TreeNode* root) {
        
        vector<vector<int>> ans;
        if(root==nullptr)return ans;
        queue<TreeNode*>q;
        q.push(root);
        while(!q.empty()){
            int size = q.size();
            vector<int> level;
            for(int i=0;i<size;i++){
                TreeNode* node = q.front();
                q.pop();
                level.push_back(node->data);
                if(node->left != nullptr) q.push(node->left);
                if(node->right != nullptr) q.push(node->right);
            }
            ans.push_back(level);
        }
        return ans;
    }
};
```
Time Complexity: O(N)
