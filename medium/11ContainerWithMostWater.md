## [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

#### 题目大意

给定数字数组，求数字区间的最大矩形面积，长是数组间距离，高是两个数字的小值。

从两侧往中间遍历，每次移动小的那个，因为小的那个移动大概率会让面积变大。

```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxa = 0,area = 0;
        int l = 0, r = height.size() - 1;
        while(l < r){
            if(height[r] < height[l]) {
                area = height[r] * (r- l);
                r--;
            }else {
                area = height[l] * (r- l);
                l++;
            }
            if(area > maxa) maxa = area;
        }
        return maxa;
    }
};
```
