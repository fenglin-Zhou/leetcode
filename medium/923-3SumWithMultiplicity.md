## [923. 3Sum With Multiplicity](https://leetcode.com/problems/3sum-with-multiplicity/)

#### 题目大意

给你一串排好序的数组和一个目标值，求3个数组成目标值的所有组合数，同时一个数字只能出现一次。

先统计出所有数字出现的次数，双循环遍历，一个从头开始，另一个从第一个循环的值开始。i和j就是他们的值，k就是target-i-j。如果k不存在那么就跳出去，如果i=j=k，那么就是相同的值，那就是选三个，如果这个值只出现一次，在数列选的时候有0直接就没算不会出现问题。如果i=j，那么就是选i和j，再乘k。如果都不同，那就三个相乘。

```
class Solution {
public:
    int threeSumMulti(vector<int>& arr, int target) {
        map<int, long> mp;
        long ans = 0;
        for(auto num : arr){
            mp[num]++;
        }
        for(auto it : mp){
            for(auto it1 : mp){
                int i = it.first, j = it1.first, k = target-i-j;
                if(!mp.count(k)) continue;
                if(j==i && j==k) ans += mp[i] * (mp[i] - 1) * (mp[i] - 2) / 6;
                else if(i == j && j != k) ans += mp[i] * (mp[i] - 1) / 2 * mp[k];
                else if(i < j && j < k) ans += mp[i] * mp[j] * mp[k];
            }
        }
        return ans % (int)(1e9 + 7);
    }
};
```

```
class Solution {
public:
    int threeSumMulti(vector<int>& arr, int target) {
        int f[101] = {};
        for (auto x: arr)
            ++f[x];
        uint64_t ans = 0;
        for (int i = 0; i <= 100; ++i) {
            for (int j = i; j <= 100; ++j) {
                int k = target - i - j;
                if (k < j || k > 100)
                    continue;
                ans += 
                    i == j && j == k ? (1l * f[i] * (f[i] - 1) * (f[i] - 2) / 6) :
                    i == j ? 1l * f[i] * (f[i] - 1) / 2 * f[k] :
                    j == k ? 1l * f[i] * f[j] * (f[j] - 1) / 2 :
                    1l * f[i] * f[j] * f[k];
            }
        }
        return ans % int(1e9 + 7);
    }
};
```
