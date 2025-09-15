### Preorder Traversal

**Problem:** Given root of binary tree, return the preorder traversal of the binary tree.

**Code:**
```cpp
class Solution{
	public:
        void solve(TreeNode* node, vector<int>&ans){
            if(node == nullptr) return;
            ans.push_back(node->data);
            solve(node->left, ans);
            solve(node->right,ans);
        }
		vector<int> preorder(TreeNode* root){
           vector<int> ans;
           solve(root,ans);
           return ans;
		}
};
```
Time Complexity: O(N)
