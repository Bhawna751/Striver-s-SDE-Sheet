### Inorder Traversal

**Problem:** Given root of binary tree, return the Inorder traversal of the binary tree.

**Code:**
```cpp
class Solution{
	public:
        void inorder(TreeNode* root, vector<int>&ans){
            if(root==nullptr) return;
            inorder(root->left,ans);
            ans.push_back(root->data);
            inorder(root->right,ans);
        }
		vector<int> inorder(TreeNode* root){
	        
            vector<int>ans;
            inorder(root,ans);
            return ans;
		}
};
```
Time Complexity: O(n)
