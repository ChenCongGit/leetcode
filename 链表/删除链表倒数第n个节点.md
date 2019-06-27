# 删除链表的倒数第N个节点
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

####示例：
  ```cpp
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**代码**
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        
        // 定义伪头结点，减少特殊情况
        ListNode * firstNode = new ListNode(0);
        firstNode->next = head;
        
        ListNode * iterNode_1 = firstNode;
        ListNode * iterNode_2 = firstNode;
        
        // 第二个指针比第一个指针多n+1
        for (int i = 0; i < n + 1; i++)
        {
            iterNode_2 = iterNode_2->next;
        }
        while (iterNode_2 && iterNode_1)
        {
            iterNode_1 = iterNode_1->next;
            iterNode_2 = iterNode_2->next;
        }
        iterNode_1->next = iterNode_1->next->next;
        return firstNode->next;
    }
};
```
**这个题采用双指针策略我们首先设置一个伪头结点，这样能够减少原来头结点的特殊情况，我们设置两个指针，其中一个初始指向伪头结点，另一个指针初始指向伪头结点之后的第n个节点，然后一起前进，当第二个节点指向最后的空节点时，第一个指针此时将指向倒数第n+1个节点（注意我们要找到的是倒数第n个节点的前一个结点，因为这样才能跳过倒数第n个结点），最后我们再返回我们伪头结点的下一个节点，即原始头结点。**


