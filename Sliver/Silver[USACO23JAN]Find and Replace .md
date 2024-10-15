# [USACO23JAN] Find and Replace
原题link: https://usaco.org/index.php?page=viewproblem2&cpid=1278

同源金组题:https://usaco.org/index.php?page=viewproblem2&cpid=1281

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

The last input string can be changed into its output string like so: 𝙰𝙱𝙲𝙳→𝙴𝙱𝙲𝙳→𝙴𝙰𝙲𝙳→𝙱𝙰𝙲𝙳 ABCD→EBCD→EACD→BACD.

#### SCORING:

- Inputs 2-6: Every string has a length at most 5050.
- Inputs 7-9: All strings consist only of lowercase letters '𝚊a' through '𝚎e'
- Inputs 10-15: No additional constraints.

Problem credits: Benjamin Qi

```
def char_to_index(char):
    return ord(char) - ord('A') + 1 if char.isupper() else ord(char) - ord('a') + 27

def main():
    test_cases = int(input())  # 输入测试数据的数量
    for _ in range(test_cases):
        mapping = [0] * 53  # 存储字符映射关系
        indegree = [0] * 53  # 存储每个字符的入度
        start_group = [0] * 53  # 用于环检测

        source_string = input().strip()  # 输入源字符串
        target_string = input().strip()  # 输入目标字符串

        target_set = set()  # 存储目标字符的集合
        is_convertible = True  # 标记是否可转换
        is_same = True  # 标记是否所有字符相同
        length = len(source_string)  # 字符串长度

        for i in range(length):
            source_index = char_to_index(source_string[i])
            target_index = char_to_index(target_string[i])
            if mapping[source_index] and mapping[source_index] != target_index:
                is_convertible = False  # 同一源字符指向不同目标字符
                break
            mapping[source_index] = target_index  # 更新映射关系
            target_set.add(target_index)  # 添加目标字符到集合
            if source_string[i] != target_string[i]:
                is_same = False  # 标记字符不同

        if len(target_set) == 52 and not is_same:
            is_convertible = False  # 所有字符都不同且不可转换

        if not is_convertible:
            print("-1")
            continue

        if is_same:
            print("0")
            continue

        operation_count = 0  # 记录需要的操作数
        for i in range(1, 53):
            if mapping[i] and mapping[i] != i:
                operation_count += 1
                indegree[mapping[i]] += 1

        for i in range(1, 53):
            current = i
            if start_group[current]:
                continue
            while current and not start_group[current]:
                start_group[current] = i  # 标记同一环
                current = mapping[current]
            if current and current != mapping[current] and start_group[current] == i:
                has_multiple_indegree = False  # 标记是否有多重入度
                cycle_node = current
                while True:
                    if indegree[cycle_node] > 1:
                        has_multiple_indegree = True
                    cycle_node = mapping[cycle_node]
                    if cycle_node == current:
                        break
                if not has_multiple_indegree:
                    operation_count += 1  # 增加操作数

        print(operation_count)

if __name__ == "__main__":
    main()
```

