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
**【简单】【53. 最大子序和】**

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
>输入: [-2,1,-3,4,-1,2,1,-5,4]

>输出: 6

>解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
### 2. 解题思路
**i**时刻最大子序列和 = **i-1**时刻最大子序列和与0中较大值 + 当前的值
`sum[i]= nums[i] + max(sum[i-1], 0)`
整个数组的最大子序列和为`max(sum)`
### 3. 提交代码
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            nums[i]= nums[i] + max(nums[i-1], 0)
        return max(nums)
```
### 4. 注意事项
1. 
### 5. 其他代码
```python
code block
```
## 第三题
### 1. 题目描述
**【简单】【70. 爬楼梯】**

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

### 2. 解题思路
递归问题

### 3. 提交代码
1. ```python
   class Solution:
       def climbStairs(self, n: int) -> int:
           if n == 1:
               return 1
           if n == 2:
               return 2
           else:
               a = self.climbStairs(n-1) + self.climbStairs(n-2)
           return a
   ```
2. ```python
   class Solution:
       def climbStairs(self, n: int) -> int:
           nums=[]
           nums.append(1)
           nums.append(2)
           if n>2:
               for i in range(2,n,1):
                   nums.append( nums[-1] + nums[-2] )
           return nums[n-1]
   ```

### 4. 注意事项
1. 直接采用递归计算会超时
2. 因为知道了递推公式可以采用正向计算，减少重复计算量
### 5. 其他代码
```python
code block
```
## 第四题
### 1. 题目描述
**【简单】【121. 买卖股票的最佳时机】**

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

### 2. 解题思路
第i天的最大获利 = max(第i-1天的最大获利,第i天价格-前i-1天的最低价格）

### 3. 提交代码
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        """
        gain_price = [0]
        l=len(prices)
        for i in range(1,l,1):#前后两天的差值
            gain_price.append(prices[i]-prices[i-1])
        for i in range(1, l):#求连续子序列的最大和
            gain_price[i]= gain_price[i] + max(gain_price[i-1], 0)
        return max(gain_price)
        """
        l=len(prices)
        if l<2:
            return 0
        else:
            minp = prices[0]
            maxp = 0
            l=len(prices)
            for i in range(1,l):
                if minp>prices[i]:
                    minp = prices[i]
                maxp = max(maxp,prices[i]-minp)
            return maxp
```
### 4. 注意事项
1. 如果将股票价格转换为相邻两天的差，那么原问题等价于求最大子序列的和
### 5. 其他代码
```python
code block
```
## 第五题
### 1. 题目描述
**【简单】【231. 2的幂】**

给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

### 2. 解题思路
位运算符的使用
例如8的二进制表示：1000（2的幂只有一位为1，其余均为0）
7：0111
### 3. 提交代码
```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        """
        while(True):
            if n>=0 and n<1:
                return False
                break
            elif n == 1:
                return True
                break
            else:
                n = n/2
         """
        return n>0 and (not (n&(n-1))) #例子，8：1000，7:0111 
```
### 4. 注意事项
1. 
### 5. 其他代码
```python
code block
```
## 第六题
### 1. 题目描述
**【中等】【3. 无重复字符的最长子串】**

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

### 2. 解题思路

前i个字符串的最大不重复子串 = max(前i-1个字符串的最大不重复子串,当前字符加入后计算的长度L）
如果当前符号之前出现过，L = max(当前位置-最近一次出现的位置，当前位置-子字符串的起始位置）

### 3. 提交代码
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        L = len(s)
        Str = {} #存放字符及其最近一次出现位置
        pos = 0
        count = 0
        for i in range(L):
            if s[i] in Str :
                pos = max( Str[s[i]], pos )#字符出现后，计算的起始位置就改为出现位置的后一位
            count = max( count, i - pos + 1 )
            Str[s[i]] = i + 1
        return count
```
### 4. 注意事项
1. 
### 5. 其他代码
```python
code block
```