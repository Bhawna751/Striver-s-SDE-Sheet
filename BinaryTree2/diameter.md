### Diameter of a tree

**Problem:** Given the root of a binary tree, return the length of the diameter of the tree.

**Brute:** 
- diameter = left subtree h + right subtree h
- max(diameter, max(diameter of left, diameter of right))

```cpp
class Solution {
public:
    int height(TreeNode* node){
        if(node==nullptr)return 0;
        return 1 + max(height(node->right), height(node->left));
    }
    int diameterOfBinaryTree(TreeNode* root) {
        int d=0;
        if(root==nullptr)return 0;
        int lefth = height(root->left);
        int righth = height(root->right);
        d=lefth + righth;
        int leftdia = diameterOfBinaryTree(root->left);
        int rightdia = diameterOfBinaryTree(root->right);
        return max(d,max(leftdia, rightdia));
    }
};
```
Time Complexity: O(N x N)

**Optimal:**
```cpp
class Solution {
public:
    int height(TreeNode*node, int &d){
        if(node==nullptr)return 0;
        int lefth = height(node->left, d);
        int righth = height(node->right, d);
        d = max(d,lefth + righth);
        return 1 + max(lefth,righth);
    }
    int diameterOfBinaryTree(TreeNode* root) {
        int d=0;
        height(root,d);
        return d;        
    }
};
```
Time Complexity : O(N)
