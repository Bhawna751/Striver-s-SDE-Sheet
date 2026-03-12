### Right/Left View of BT
- use an empty queue and a 2d array
- while(!q.empty())
    - remember the size of q (representing the number of nodes at cur level)
    - create a vector to store nodes at curernt level
    - for each node at lvl, dequeue the node from queue, add it's val to lvl vector, enqueue left and right children of the cur node.
    - after processing all nodes at lvl, add the lvl vector to the array
- simply store the first node of each lvl vector for left view and the last node for right view.

```cpp
class Solution {
public:
    vector<vector<int>> solve(TreeNode *root){
        vector<vector<int>> ans;
        if(!root)return ans;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int n = q.size();
            vector<int> lvl;
            for(int i=0;i<n;i++){
                TreeNode *cur = q.front();
                lvl.push_back(cur->val);
                q.pop();
                if(cur->left!=nullptr)q.push(cur->left);
                if(cur->right!=nullptr)q.push(cur->right);
            }
            ans.push_back(lvl);
        }
        return ans;
    }
    vector<int> rightSideView(TreeNode* root) {
     vector<int> ans;
     vector<vector<int>> lvlorder = solve(root);
     for(auto it:lvlorder){
        ans.push_back(it.back());
     }   
     return ans;
    }
};
```
