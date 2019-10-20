## 19.[删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.  
说明：
给定的 n 保证是有效的。

思路：
1. 遍历两遍，先得到链表长度，再移除指定节点：  
    ```python
    # Definition for singly-linked list.
    class ListNode:
        def __init__(self, x):
            self.val = x
            self.next = None

    class Solution:
        def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
            headNode = ListNode(0)
            headNode.next = head
            firstList = head
            index = 0
            while firstList:
                index +=1
                firstList = firstList.next
            length = index - n
            firstList = headNode
            while length > 0:
                length -= 1
                firstList = firstList.next
            firstList.next = firstList.next.next

            return headNode.next  
                
    ```
    虽然AC，却很丑陋 

2. 只遍历一遍  
   使用一快一慢两个指针，相隔N个节点，遍历一遍。快指针到达链表尾时，慢指针也就处在倒数N个节点处。神奇的是尝试用这种方法，执行速度不如遍历两次来的好，姑且作为一种思路
   ```python
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        fast,slow = dummy,dummy
        for  i in range(n+1):
            fast = fast.next
        while fast is not None: 
            fast = fast.next
            slow = slow.next
        slow.next = slow.next.next
        return dummy.next
   ```
   

## 20.[有效的括号](https://leetcode-cn.com/problems/valid-parentheses)
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

思路：利用辅助栈判断有效字符串

### 算法
* 初始化栈 S。
* 一次处理表达式的每个括号。
* 如果遇到开括号，我们只需将其推到栈上即可。这意味着我们将稍后处理它。
* 如果我们遇到一个闭括号，那么我们检查栈顶的元素。如果栈顶的元素是一个**相同类型**的**左括号**，那么我们将它从栈中弹出并继续处理。否则，这意味着表达式无效。
* 如果到最后我们剩下的栈中仍然有元素，那么这意味着表达式无效。

在Python中，可以通过字典简化程序——在哈希表中进行搜索操作节省资源
```python
class Solution:
    def isValid(self, s: str) -> bool:
        mapping = {')':"(", ']':'[', '}':'{'}
        stack = []
        n = len(s)
        for char in s:
            if char in mapping: #如果是左括号，弹出栈顶元素进行判断
                top = stack.pop() if stack else '1'
                if top != mapping[char]: #如果括号不匹配，返回False
                    return False
            else:
                stack.append(char) #如果是右括号，压入栈中
            if len(stack)>n/2: #加上额外的判断减少了8ms运行时间
                return False
        return True if not stack else False
```
