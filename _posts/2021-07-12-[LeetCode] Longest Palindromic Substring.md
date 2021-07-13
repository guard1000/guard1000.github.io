---
layout: posts
title:  "[LeetCode] Longest Palindromic Substring"
categories: ['Algorithm', 'LeetCode']


---

[문제링크](https://leetcode.com/problems/longest-palindromic-substring/)

<br/>

###### 문제 설명

Given a string `s`, return *the longest palindromic substring* in `s`.

 

**Example 1:**

```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```
Input: s = "a"
Output: "a"
```

**Example 4:**

```
Input: s = "ac"
Output: "a"
```

 

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters (lower-case and/or upper-case),



<br/>

### Sol

옛날옛날 학부 1학년 처음 들었던 C언어 전공수업에서 처음으로 챌린징(?) 했던 녀석이 바로 이 Palindrome 이었던 기억이 납니다. 그리고 시간이 흘러 알고리즘 인터뷰를 준비하거나, 코테를 준비하면서도 잊을만할때 찾아오는 주제이기도 하네요. ㅎㅎ  다행인 건 이제는 어렵다는 느낌보단 반갑다는 느낌이 들 정도로 미운정이 들었나 봅니다 : )

<br/>

이 문제에서는 먼저, 입력된 s가 1글자로 이루어져 있을 경우, 바로 s를 반환시켜 버렸습니다.

이제 Palindrome이 짝수의 길이로 생성될 수도 있고, 홀수의 길이로 생성될 수도 있기 때문에,

경우의 수를 나누어 풀이를 진행했습니다.

물론, 짝수인 경우와 홀수인 경우를 확인하여 결국 가장 긴 palindrome을 answer로 반환합니다!

<br/>

![image](C:\Program Files\Typora\2021-07-12-[LeetCode] Longest Palindromic Substring\[LeetCode] Longest Palindromic Substring_1.png)

1. 위와 같이, idx 위치를 기준으로, 짝수인경우엔 그냥 idx 전까지와 idx부터를 나누어 palindrome인지를 확인하면 됩니다.

2. 홀수길이의 palindrome을 확인하고자 하면, idx 위치는 제외하고 양 옆을 분할하여 palindrome인지 여부를 확인하였습니다.



아래 코드를 통해 확인해 봅시다.

<br/>

### Code

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if len(s) == 1:
            return s
        s = list(s)
        # 짝수
        idx, n, answer = 1, 0, ''
        while idx < len(s):
            a, b = s[:idx], s[idx:]
            a.reverse()

            l = min(len(a), len(b))
            tmp = ''
            for i in range(l):
                if a[i] != b[i]:
                    break
                else:
                    tmp = a[i] + tmp + b[i]
            if len(tmp) > n:
                answer = tmp
                n = len(answer)
            idx += 1

        # 홀수
        idx = 1
        while idx < len(s):
            a, b = s[:idx], s[idx+1:]
            a.reverse()

            l = min(len(a), len(b))
            tmp = s[idx]
            for i in range(l):
                if a[i] != b[i]:
                    break
                else:
                    tmp = a[i] + tmp +b[i]
            if len(tmp) > n:
                answer = tmp
                n = len(answer)
            idx += 1

        if answer == '':
            return s[0]

        return answer
```



