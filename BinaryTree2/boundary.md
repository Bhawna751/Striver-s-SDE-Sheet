### Boundary Traversal

**Problem:**
Given a root of Binary Tree, perform the boundary traversal of the tree. 

The boundary traversal is the process of visiting the boundary nodes of the binary tree in the anticlockwise direction, starting from the root.

The boundary of a binary tree is the concatenation of the root, the left boundary, the leaves ordered from left-to-right, and the reverse order of the right boundary.

The left boundary is the set of nodes defined by the following:
- The root node's left child is in the left boundary. If the root does not have a left child, then the left boundary is empty.
- If a node in the left boundary and has a left child, then the left child is in the left boundary.
- If a node is in the left boundary, has no left child, but has a right child, then the right child is in the left boundary.
- The leftmost leaf is not in the left boundary.


The right boundary is similar to the left boundary, except it is the right side of the root's right subtree. Again, the leaf is not part of the right boundary, and the right boundary is empty if the root does not have a right child.

**Approach:**
- create ans vector, check if root is null and return ans
- if root is leaf node add root->val to ans
- find the left boundary
- find the leaf nodes
- find the right boundary and reverse it before adding to ans vector

```cpp
class Solution{
public:
    bool leaf(TreeNode* root){
        return !root->left && !root->right;
    }
    void addLeftBoundary(TreeNode* node, vector<int> &ans){
        TreeNode* q = node->left;
        while(q){
            if(!leaf(q))ans.push_back(q->data);
            if(q->left)q=q->left;
            else q=q->right;
        }
    }
    void addRightBoundary(TreeNode* node, vector<int> &ans){
        TreeNode* q = node->right;
        vector<int>temp;
        while(q){
            if(!leaf(q))temp.push_back(q->data);
            if(q->right)q=q->right;
            else q=q->left;
        }
        for(int i=temp.size()-1;i>=0;i--){
            ans.push_back(temp[i]);
        }
    }
    void leafNodes(TreeNode* root, vector<int>&ans){
        if(leaf(root)){
            ans.push_back(root->data);
            return;
        }
        if(root->left)leafNodes(root->left,ans);
        if(root->right)leafNodes(root->right, ans);
    }
    vector <int> boundary(TreeNode* root){
    	vector<int>ans;
        if(root==nullptr)return ans;
        if(!leaf(root))ans.push_back(root->data);
        addLeftBoundary(root,ans);
        leafNodes(root,ans);
        addRightBoundary(root,ans);
        return ans;
    }
};
```
Time Complexity: O(N)
