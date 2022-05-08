## [341. Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/)

#### 题目大意

给定一个数组嵌套，改成一个正常数组。直接dfs遍历把数组放到vector。

```
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */

class NestedIterator {
public:
    vector<int> nums;
    int index;
    NestedIterator(vector<NestedInteger> &nestedList) {
        for(auto &num : nestedList){
            if(num.isInteger()){
                nums.push_back(num.getInteger());
            }else{
                dfs(num.getList());
            }
        }
        index = 0;
    }
    void dfs(vector<NestedInteger> &nestedList){
        for(auto &num : nestedList){
            if(num.isInteger()){
                nums.push_back(num.getInteger());
            }else{
                dfs(num.getList());
            }
        }
    }
    int next() {
        if(index < nums.size())
            return nums[index++];
        return INT_MIN;
    }
    
    bool hasNext() {
        return index < nums.size();
    }
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```
