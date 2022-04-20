## [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)

#### 题目大意

实现二叉搜索树的迭代器。

直接用队列存了，用空间换时间。

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
class BSTIterator {
public:
    BSTIterator(TreeNode* root) {
        dfs(root);
    }
    queue<TreeNode*> q;
    void dfs(TreeNode *root){
        if(root==nullptr) return;
        dfs(root->left);
        q.push(root);
        dfs(root->right);
    }
    
    int next() {
        if(!q.empty()){
            TreeNode* ans = q.front();
            q.pop();
            return ans->val;
        }
        return INT_MIN;
    }
    
    bool hasNext() {
        return !q.empty();
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```
