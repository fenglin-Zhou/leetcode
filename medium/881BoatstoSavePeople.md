## [881. Boats to Save People](https://leetcode.com/problems/boats-to-save-people/)

#### 题目大意

给一列人的体重，给一个船的limit，一个船只能载两人，问最少多少艘船。

直接一个循环，从最后往前，匹配一下最小值，能就少一个人不能就算了。

```
class Solution {
public:
    int numRescueBoats(vector<int>& people, int limit) {
        sort(people.begin(), people.end());
        int ans = 0;
        int i = 0;
        int j = people.size() - 1;
        while(i <= j){
            if(people[j] + people[i] <= limit){
                j--;
                i++;
            }else{
                j--;
            }
            ans++;
        }
        return ans;
    }
};
```
