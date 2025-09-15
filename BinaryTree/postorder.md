### Postorder Traversal

**Problem:** Given root of binary tree, return the postorder traversal of the binary tree.

**Code:** 
```cpp
class Solution{
	public:
        void solve(TreeNode* node, vector<int>&ans){
            if(node == nullptr) return;
            solve(node->left, ans);
            solve(node->right,ans);
            ans.push_back(node->data);
        }
		vector<int> postorder(TreeNode* root){
           vector<int> ans;
           solve(root,ans);
           return ans;
		}
};
```
Time Complexity: O(N)
