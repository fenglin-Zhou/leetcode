## [99. Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)

#### 题目大意

给一个二叉搜索树，但是里面只有两个节点的值被交换位置了，需要我们复原，就是把那两个节点的值换一下。这个题本身难度是medium，但是我没做出来。。。所以放到hard。

二叉搜索树特点是左节点小于当前值，右节点大于。按照中序遍历的规则，前面的值一定是小于后面的，那么我们就可以根据这一规则来，中序遍历的中间进行我们的比对。

首先需要三个值，first，second用来保存需要交换的两个值。pre用来存储上一个值，也就是当前位置的上一个值，因为这个pre值一定是小于当前值的。如果他大于了，那就是要交换的值的其中一个。以此类推下一次遇到这个情况就是另一个要交换的值。

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode *first;
    TreeNode *second;
    TreeNode *pre;
    void recoverTree(TreeNode* root) {
        first = second = pre = nullptr;
        recover(root);
        swap(first->val, second->val);
    }
    void recover(TreeNode *root){
        if(root == nullptr) return;
        recover(root->left);
        
        if(first == nullptr && pre != nullptr && pre->val >= root->val)
            first = pre;
        
        if(first != nullptr && pre->val >= root->val)
            second = root;
        
        pre = root;
        
        recover(root->right);
    }
};
```
