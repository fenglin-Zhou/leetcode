## [82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

给定一个排序链表的头部，删除所有具有重复数字的节点，只留下原始链表中不同的数字。返回排序好的链表。

添加一个新的头用来引导，中间一个变量保存相同值的大小，判断到相同的点记录下值，下一个继续判断是否等于duplicate，因为可能存在连续三个相同的值。

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;
        int duplicate;
        while (cur->next && cur->next->next) {
            if (cur->next->val == cur->next->next->val) {
                duplicate = cur->next->val;
                while (cur->next && cur->next->val == duplicate) 
                    cur->next = cur->next->next;
            }
            else cur = cur->next;
        }
        return dummy->next;
    }
};
```
