# 栈 stack

- Stack 先入后出 FILO（First In Last Out）
- 查询的时间复杂度为O(n)
- 插入和删除栈顶的时间复杂度为O(n)





## 20.有效的括号

```
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:

输入: "()"
输出: true
示例 2:

输入: "()[]{}"
输出: true
示例 3:

输入: "(]"
输出: false
示例 4:

输入: "([)]"
输出: false
示例 5:

输入: "{[]}"
输出: true

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-parentheses
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

### 解法 stack

```go
package main

import "fmt"

func isValid(s string) bool {
	//如果为单数则假设均不成立
	if len(s)%2 == 1 {
		return false
	}
	hash := map[byte]byte{')': '(', ']': '[', '}': '{'}
	stack := make([]byte, 0)
	for i := 0; i < len(s); i++ {
		val, ok := hash[s[i]]
		//左括号入栈
		if s[i] == '(' || s[i] == '[' || s[i] =='{'{
			stack = append(stack, s[i]) //入栈
		} else if len(stack) > 0 && ok && val == stack[len(stack)-1] { //栈不为空并且能获取到对应的哈希值，比对获取的哈希值是否与栈顶值相等
			//如果相等则将栈顶值进行出栈
			stack = stack[:len(stack)-1]
		} else {
			return false
		}
	}

	return len(stack) == 0
}

func main() {
	fmt.Println(isValid("(){}1{}()"))
	fmt.Println(isValid("()"))
}

```



