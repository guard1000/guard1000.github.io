---
layout: posts
title:  "[LeetCode] Letter Combinations of a Phone Number"
categories: ['Algorithm', 'LeetCode']



---

[문제링크](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

<br/>

###### 문제 설명

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](C:\Program Files\Typora\2021-07-15-[LeetCode] Letter Combinations of a Phone Number\200px-Telephone-keypad2.svg.png)

 

**Example 1:**

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Example 2:**

```
Input: digits = ""
Output: []
```

**Example 3:**

```
Input: digits = "2"
Output: ["a","b","c"]
```

 

**Constraints:**

- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

<br/>



### Sol

최근 순열과 조합을 활요한 경우의 수 문제를 몇 번 다루었습니다.

이 문제는 '중복'이 있는 순열을 활용하여, python으로 코테를 준비하는 분들이 활용하기 좋은 itertools의 활용성을 확인하고자 다뤄 보겠습니다.

문제 자체의 난이도는 Easy 같은 Medium으로, 제 풀이말고도 충분히 더 효율적인 풀이가 가능할 것으로 보입니다.

<br/>

먼저, dictionary로 어떤 버튼을 누를때 가능한 리스트를 선언해 두었습니다.

이후, 각 버튼에서 idx 번을 눌렀을 때 나오는 문자를 생성하도록 중복순열(product)을 생성했습니다.

<br/>

예를들어, digits 가 "23" 들어온 경우,

버튼 2 에서 생성가능한 dic[2] : ['a','b','c'] 와

버튼 3에서 생성가능한 dic[3] : ['d','e','f'] 에 대해, product를 생성해 주면,

(0,0), (0,1), (0,2), (0,3), (1,0), (1,1), (1,2), (1,3), (2,0) ... 와 같이 생성됩니다.

dic[2]와 dic[3] 은 len(dic[2]), len(dic[2]) 이 모두 3 이므로, idx가 3이 아닌 경우,

ad, ae, af, bd, be, bf, cd, ce, cf를 생성해 answer에 추가하게 됩니다.



<br/>

이를 코드로 구현하면 다음과 같습니다.



### Code

```python
import itertools
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        answer = []
        dic = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z']
        }
        answer = []
        digits = list(digits)
        
        idxs = [0,1,2,3]
        if len(digits) == 1:
            answer = dic[digits[0]]
        
        elif len(digits) >= 2:
            mypermutation = itertools.product(idxs, repeat=len(digits))
            for myperm in mypermutation: # (0, 3, 2)
                tmp, idx = '', 0
                while idx < len(digits) and len(dic[digits[idx]]) > myperm[idx]:
                    tmp += dic[digits[idx]][myperm[idx]]
                    idx += 1
                
                if idx == len(digits):
                    answer.append(tmp)
                    
        return answer
```





