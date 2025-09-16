### Maxximum Path Sum

**Problem:** In a binary tree, a path is a list of nodes where there is an edge between every pair of neighbouring nodes. A node may only make a single appearance in the sequence.

The total of each node's values along a path is its path sum. Return the largest path sum of all non-empty paths given the root of a binary tree.

Note: The path does not have to go via the root.

**Approach:**
- recursive function designed to calculate the maximum path sum for each subtree rooted at a given node.
- If the current node is null, return 0.
- Proceed by calculating the maximum path sum for both the left and right subtrees. If the path sum for either subtree is negative, it should be disregarded.
- For each node, compute the potential maximum path sum that passes through the node and its children. This sum includes the node itself and the maximum path sums from both subtrees. If this value exceeds the current global maximum sum, update the global maximum to reflect this new higher value.
- Finally, return the maximum path sum for the current node, considering only one of its subtrees. This step ensures that when the function backtracks up the tree, only the highest path sum from either the left or right subtree is propagated upward, maintaining the integrity of the overall maximum path sum calculation.

```cpp
class Solution {
public:
    int solve(TreeNode* node, int &maxi){
        if(node==nullptr)return 0;
        int left = max(0,solve(node->left, maxi));
        int right = max(0,solve(node->right, maxi));
        maxi = max(maxi, left+right+node->val);
        return max(left,right) + node->val;
    }
    int maxPathSum(TreeNode* root) {
        int maxi=-1e9;
        solve(root, maxi);
        return maxi;
    }
};
```
Time Complexity: O(N)
