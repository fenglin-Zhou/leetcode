## [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

#### 题目大意

给一个链表，里面除了next，还有一个random随机指针指向链表中的某个节点，需要去深度复制。

思路是一个map保存每个原始节点对应相应的新节点，这样我们就可以对random赋值是通过map找到相对应的节点地址，直接进行赋值。需要两个循环，一个用来构建链表，另一个用来赋值random指针。

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head == nullptr) return nullptr;
        map<Node*, Node*> nodemap;
        Node* temp = head;
        Node* newhead = new Node(head->val);
        nodemap[head] = newhead;
        Node* newtemp = newhead;
        // int i = 0;
        while(temp->next != nullptr){
            temp = temp->next;
            newtemp->next = new Node(temp->val);
            newtemp = newtemp->next;
            nodemap[temp] = newtemp;
            // i++;
        }
        // cout << i << " ";
        // i = 0;
        temp = head;
        newtemp = newhead;
        Node* pos = nullptr;
        while(temp != nullptr){
            pos = nodemap[temp->random];
            newtemp->random = pos;
            newtemp = newtemp->next;
            temp = temp->next;
            // i++;
        }
        // cout << i << " ";
        return newhead;
    }
};
```
