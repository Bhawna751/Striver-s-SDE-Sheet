### Maximum Depth in Binary Tree

**Problem:** Given root of the binary tree, return its maximum depth.

**Recursive:** 
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==nullptr)return 0;
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);
        return 1+max(left,right);
    }
};
```
Time Complexity: O(N)

**Iterative:**
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==nullptr)return 0;
        queue<TreeNode*>q;
        q.push(root);
        int lvl = 0;
        while(!q.empty()){
            int size = q.size();
            for(int i=0;i<size;i++){
                TreeNode* front = q.front();
                q.pop();
                if(front->left!=nullptr) q.push(front->left);
                if(front->right != nullptr)q.push(front->right);
                
            }
            lvl++;
        }
        return lvl;
    }
};
```
