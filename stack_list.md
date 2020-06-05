==题目描述==

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

示例:

s = "3[a]2[bc]", 返回 "aaabcbc".
s = "3[a2[c]]", 返回 "accaccacc".
s = "2[abc]3[cd]ef", 返回 "abcabccdcdcdef".

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/decode-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

==心得aspired by dalao lucifer==

心得吧：以']'作为判断条件，由里向外依次进行解码，解码操作中，涉及 字符的出栈、拼接，匹配判断字符'['的出栈，以及数字字符的出栈和拼接（数字可能是多位）（这里数字拼接结束跳出while后要及时转换为int型，以表征重复次数）
最后由于我们是用列表实现的，所以在做最后一层解码时，只需要把列表里的每个字符串元素join连接即可。

在做重复字符和重复次数的拼接时，完全没有考虑每次新pop出来的字符是往前拼接的！！！而且作为判断的标志字符'['也没有pop出，真·tcl。
空间复杂度由于涉及到了一个操作字符的栈，size差不多是操作数规模，所以O(N)；时间复杂度的话，也基本上是对字符串内的每个字符的一次遍历操作，同O(N)，N为字符串长度。
```python
def decodeString(s):
        
    stack = []
        
    for ss in s:
        repeatstr = ''
        repeatnum = ''
        if ss != ']':
            stack.append(ss)
        else:
            while stack and stack[-1] != '[':
                str = stack.pop()
                repeatstr = str+repeatstr
            stack.pop()
            while stack and stack[-1].isnumeric():
                repeatnum = stack.pop()+repeatnum
            repeatnum = int(repeatnum)
            new_str = repeatstr*repeatnum
            stack.append(new_str)
    return "".join(stack)
```
