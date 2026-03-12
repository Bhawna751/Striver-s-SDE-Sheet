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

Morris Inorder Traversal
----
It involves threaded tree traversal. There are three primary scenarios: 
- nodes without a child
- nodes with a left where the in-order predecessor does not have a right child
- nodes with a left where the right child of the in-order predecessor points back to the current node

**Approach:**
- initialize cur = root
- while (cur!=null)
  - if the cur node lacks a left child, print it's value and move to right
  - if cur has left child
    - identify the in-order predecessor of cur node which is the right most node of left subtree
    - if the right child is null then create a thread between cur node and it's right child, and move to the left
    - if the right child is not null (a thread exists), revert it by setting right  child to null, print the cur node and move to the right.

````cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        TreeNode* cur = root;
        while (cur != nullptr) {
            if (cur->left == nullptr) {
                ans.push_back(cur->val);
                cur = cur->right;
            } else {
                TreeNode* prev = cur->left;
                while (prev->right != cur && prev->right) {
                    prev = prev->right;
                }
                if (prev->right == nullptr) {
                    prev->right = cur;
                    cur = cur->left;
                } else {
                    prev->right = nullptr;
                    ans.push_back(cur->val);
                    cur = cur->right;
                }
            }
        }
        return ans;
    }
};
`````
