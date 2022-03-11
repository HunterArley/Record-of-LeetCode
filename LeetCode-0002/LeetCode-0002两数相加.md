# 两数相加

给你两个非空的链表，表示两个非负的整数。它们每位数字都是按照逆序的方式存储的，并且每个节点只能存储一位数字。
请你将两个数相加，并以相同形式返回一个表示和的链表。
你可以假设除了数字0之外，这两个数都不会以0开头。

![](assets/LeetCode-0002两数相加-a9a3dda3.png)

示例1：

```
输入： l1 = [2,4,3], l2 = [5,6,4]
输出： [7,0,8]
解释： 342 + 465 = 807
```

示例2：

```
输入： l1 = [0], l2 = [0]
输出： [0]
```

示例3：

```
输入： l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出： [8,9,9,9,0,0,0,1]
```

提示：
- 每个链表中的节点数在范围[1,100]内
- 0 <= Node.val <= 9
- 题目数据保证列表表示的数字不含前导零

# 我的代码

自己梳理了一个思路，但是代码没有实现。因为自己对链表不熟悉，需要加强基础能力。认识到了自己的不足之处。

# 思路与算法
由于输入的两个链表都是逆序存储数字的位数的，因此两个链表中同一个位置的数字可以直接相加。

同时遍历两个链表，逐位计算它们的和，并与当前位置的进位值相加。具体而言，如果当前两个链表处相应位置的数字为n1，n2，进位值为carry，则它们的和为n1+n2+carry；其中，答案链表处相应位置的数字为（n1+n2+carry）mod 10，而新的进位值为（n1+n2+carry）/10。

如果两个链表的长度不同，则可以认为长度短的链表的后面有若干个0。

此外，如果链表遍历结束后，有carry > 0，还需要在链表的后面附加一个节点，节点的值为carry。

```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *head = nullptr,*tail = nullptr;
        int carry = 0; //进位数
        while(l1 || l2)
        {
            int val1 = l1?l1->val:0;
            int val2 = l2?l2->val:0;
            int sum = val1+val2+carry;
            if(!head)
            {
                head = tail = new ListNode(sum%10);
            }
            else
            {
                tail->next = new ListNode(sum%10);
                tail = tail->next;
            }
            carry = sum/10;
            if(l1)
            {
                l1=l1->next;
            }
            if(l2)
            {
                l2=l2->next;
            }
        }
        if(carry>0)
        {
            tail ->next = new ListNode(carry);
        }
        return head;
    }
};
```

代码执行结果：
![](assets/LeetCode-0002两数相加-c50149e5.png)

执行结果：
![](assets/LeetCode-0002两数相加-d4b162fe.png)

### 复杂度分析

- 时间复杂度：O(max(m,n)),其中m和n分别为两个链表的长度。要遍历两个链表的全部位置，而处理每个位置只需要O(1)的时间。
- 空间复杂度：O(1)。注意返回值不计入空间复杂度。
