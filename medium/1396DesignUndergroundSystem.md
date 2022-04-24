## [1396. Design Underground System](https://leetcode.com/problems/design-underground-system/)

#### 题目大意

checkin输入id的进站时间和站名，checkout输入id出战的时间和站名。求给定站点之间的平均时长。

用两个map，一个存放id对应的入站时间和站点，在checkin的时候输入。第二个map存放入站和出站名组成的first，second是总时长和样本数量。在出站的时候通过map获取到id的入站时间，并将总时长通过出入站名定位到pair加上时长和样本数量。

获取两站之间平均时长就可以通过站点名拿到总时长和样本数相除。

```
class UndergroundSystem {
public:
    map<int, pair<string, int>> idto;
    map<string, pair<int, int>> stat;
    UndergroundSystem() {
    }
    
    void checkIn(int id, string stationName, int t) {
        idto[id] = pair<string, int>(stationName, t);
    }
    
    void checkOut(int id, string stationName, int t) {
        auto temp = idto[id];
        string str = temp.first+"_"+stationName;
        stat[str].first += (t - temp.second);
        stat[str].second += 1;
    }
    
    double getAverageTime(string startStation, string endStation) {
        string str = startStation+"_"+endStation;
        return (stat[str].first * 1.0 )/stat[str].second;
    }
};

/**
 * Your UndergroundSystem object will be instantiated and called as such:
 * UndergroundSystem* obj = new UndergroundSystem();
 * obj->checkIn(id,stationName,t);
 * obj->checkOut(id,stationName,t);
 * double param_3 = obj->getAverageTime(startStation,endStation);
 */
```
