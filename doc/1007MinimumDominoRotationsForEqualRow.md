## [1007. Minimum Domino Rotations For Equal Row](https://leetcode.com/problems/minimum-domino-rotations-for-equal-row/)

#### 题目大意

给定两行数组，求旋转交换最少次数使得两行中有一行数字全部相等。

我的方法：求出两行最多出现的数字，分别判断全在上面和下面要旋转的次数，取小的那个。

时间靠前的方法（单实际提交并不会快）：取tops[0]和bottoms[0]为固定值，分别求在上下的旋转次数，所以是有四个旋转值，最后取小的。

```
class Solution {
public:
    int minDominoRotations(vector<int>& tops, vector<int>& bottoms) {
        int size = tops.size();
        int cnt[9] = {0};
        for(int i = 0; i < size; ++i){
            cnt[tops[i]]++;
            cnt[bottoms[i]]++;
        }
        int max = cnt[0];
        int maxindex = 0;
        for(int i = 1; i < 7; ++i){
            if(max < cnt[i]){
                max = cnt[i];
                maxindex = i;
            }
        }
        int ans = 0;
        int ans1 = 0;
        for(int i = 0; i < size; ++i){
            if(tops[i] != maxindex){
                if(bottoms[i] == maxindex) ans++;
                else return -1;
            }else{
                if(bottoms[i] != maxindex) ans1++;
            }
        }
        return ans > ans1? ans1 : ans;
    }
};
```
