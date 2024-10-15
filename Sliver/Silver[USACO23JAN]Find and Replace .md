# [USACO23JAN] Find and Replace
原题link: https://usaco.org/index.php?page=viewproblem2&cpid=1278

## 题目描述

Bessie 正在使用世界上最先进最伟大的文本编辑器：miV！她想将一个仅由大写和小写英文字母组成的字符串转换为一个新的字符串。每一次操作，miV 可以将字符串中所有的字母 c1 替换成另一种字母 c2。例：对于字符串aAbBa, 如果将其中的 a 替换成 B, 那么字符串会变为BAbBB。

Bessie 非常地忙碌, 所以对于给出的 T(1≤T≤10) 组测试数据, 请输出她至少需要多少次操作才能把原字符串转换为新字符串。

【输入】

第一行是一个整数 T, 表示测试数据的数量。

接下来有 T 对长度相等的字符串。字符串中所有的字符都是大写或小写的字母。字符串的长度不会超过 105105。

【输出】

对于每组测试数据，输出转换字符串需要的最小操作数。

如果这不可能做到，输出 −1。

【输入样例】

```
4
abc
abc
BBC
ABC
abc
bbc
ABCD
BACD
```

【输出样例】

```
0
-1
1
3
```

The first input string is the same as its output string, so no keystrokes are required.

The second input string cannot be changed into its output string because Bessie cannot change one '𝙱B' to '𝙰A' while keeping the other as '𝙱B'.

The third input string can be changed into its output string by changing '𝚊a' to '𝚋b'.

The last input string can be changed into its output string like so: 𝙰𝙱𝙲𝙳→𝙴𝙱𝙲𝙳→𝙴𝙰𝙲𝙳→𝙱𝙰𝙲𝙳ABCD→EBCD→EACD→BACD.

#### SCORING:

- Inputs 2-6: Every string has a length at most 5050.
- Inputs 7-9: All strings consist only of lowercase letters '𝚊a' through '𝚎e'
- Inputs 10-15: No additional constraints.

Problem credits: Benjamin Qi

### 
