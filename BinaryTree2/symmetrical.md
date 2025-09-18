### Check for symmetrical BTs

**Problem:** Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

**Approach:**
- check  the values of left and right subtrees simultaneously
- if either subtree is null, return false, if both are null return true
- call recursively for  (left node of left subtree and right node of right subtree, right node of left subtree and left node of right subtree)

```cpp
class Solution {
public:
    bool solve(TreeNode* p, TreeNode* q){
        if(p==nullptr && q==nullptr)return true;
        if(p==nullptr || q==nullptr)return false;
        if(p->val != q->val) return false;
        return solve(p->left, q->right) && solve(p->right,q->left );
    }
    bool isSymmetric(TreeNode* root) {
        if(root==nullptr)return true;
        return solve(root->left, root->right);
    }
};
```
Time Complexity: O(N)
