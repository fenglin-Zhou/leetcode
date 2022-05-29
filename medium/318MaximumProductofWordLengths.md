## [318. Maximum Product of Word Lengths](https://leetcode.com/problems/maximum-product-of-word-lengths/)

#### 题目大意

给定字符串集合，求两个没有相同字母的字符串的数量乘积，找到最大的那个乘积。

想到了用bitmap去做，但是没想出来怎么构建bitmap，参考了别人的代码，用移位的方式让26个字母对应每个位置。然后两次for循环遍历。

```
class Solution {
public:
    int maxProduct(vector<string>& words) {
        vector<int> mask(words.size());
        int ans = 0;
        int size = words.size();
        for(int i = 0; i < size; ++i){
            for(auto c:words[i]){
                mask[i] |= 1 << (c-'a');
            }
        }
        for(int i = 1; i < size; ++i){
            for(int j = 0; j < i; ++j){
                if(!(mask[i]&mask[j])){
                    ans = max(ans, int(words[i].size() * words[j].size()));
                }
            }
        }
        return ans;
    }
};
```
