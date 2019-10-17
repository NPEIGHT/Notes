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
