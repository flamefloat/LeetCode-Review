# 第一周
## 第一题
### 1. 题目描述
**【中等】【2. 两数相加】**

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
>输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

### 2. 解题思路

1. 掌握链表的基本定义及使用
2. 考虑计算时进位的影响
3. 两个数字不等长时：添加链表长度

### 3. 提交代码
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry = 0 #进位为0
        l3 = ListNode(0)
        cur = l3
        while(True):
            
            if l1 == None :#数字不等长时，首位添零
                l1 = ListNode(0)
            if l2 == None :
                l2 = ListNode(0)
            num = (carry + l1.val + l2.val)%10
            carry = int( (carry + l1.val + l2.val)/10 )
            cur.next = ListNode(num)#链表基本使用方式，添加元素到末尾，再移动链表指针
            cur = cur.next
            l1 = l1.next
            l2 = l2.next
            if l1 == None and l2 == None :
                if carry != 0: # 确认计算完后有无进位
                    cur.next = ListNode(carry)
                    cur = cur.next
                break
        return l3.next
```
### 4. 注意事项
1. 列表中元素的查找只能通过遍历的方式查找
### 5. 其他代码
```python
code block
```
## 第二题
### 1. 题目描述
**【难度】【名称】**

### 2. 解题思路

### 3. 提交代码
```python
code block
```
### 4. 注意事项
1. 
### 5. 其他代码
```python
code block
```