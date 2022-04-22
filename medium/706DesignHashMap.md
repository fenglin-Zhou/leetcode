## [706. Design HashMap](https://leetcode.com/problems/design-hashmap/)

#### 题目大意

构建一个hashmap，采用动态链表的形式，每个哈希值一个Node，重复的值存在后面next节点。

```
struct Node {
public:
    int key;
    int val;
    Node* next;
        
    Node(int k, int v, Node* n) {
        key = k;
        val = v;
        next = n;
    }
};



class MyHashMap {
public:
    
    const static int size = 19997; // a prime number
    const static int mult = 12582917; // a prime number
    Node* data[size]; 
    
    int hash(int key) {
        return (int)((long)key * mult % size);
    }
    
    
    void put(int key, int value) {
        remove(key);
        
        int index = hash(key);
        Node* node = new Node(key, value, data[index]);
        data[index] = node;
    }
    
    int get(int key) {
        
        int index = hash(key);
        Node* node = data[index];
        
        while(node) {
            
            if(node->key == key) return node->val;
            node = node->next;
        }
        
        return -1;
    }
    
    void remove(int key) {
        
        int index = hash(key);
        Node* node = data[index];
        if(!node) return;
        
        if(node->key == key) {
            data[index] = node->next;
            return;
        }
        
        while(node->next) {  
            if(node->next->key == key) {
                node->next = node->next->next;
                return;
            }
            node = node->next;
        }
        
    }
};


/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap* obj = new MyHashMap();
 * obj->put(key,value);
 * int param_2 = obj->get(key);
 * obj->remove(key);
 */
```
