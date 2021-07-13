---
layout: posts
title:  "[백준] 괄호 제거"
categories: ['Algorithm', '백준']


---

[문제링크](https://www.acmicpc.net/problem/2800)

<br/>



# 괄호 제거

| 시간 제한 | 메모리 제한 | 제출 | 정답 | 맞은 사람 | 정답 비율 |
| :-------- | :---------- | :--- | :--- | :-------- | :-------- |
| 1 초      | 128 MB      | 2016 | 680  | 499       | 33.512%   |

<br/>

## 문제

어떤 수식이 주어졌을 때, 괄호를 제거해서 나올 수 있는 서로 다른 식의 개수를 계산하는 프로그램을 작성하시오.

이 수식은 괄호가 올바르게 쳐져 있다. 예를 들면, 1+2, (3+4), (3+4*(5+6))와 같은 식은 괄호가 서로 쌍이 맞으므로 올바른 식이다.

하지만, 1+(2*3, ((2+3)*4 와 같은 식은 쌍이 맞지 않는 괄호가 있으므로 올바른 식이 아니다.

괄호를 제거할 때는, 항상 쌍이 되는 괄호끼리 제거해야 한다.

예를들어 (2+(2*2)+2)에서 괄호를 제거하면, (2+2*2+2), 2+(2*2)+2, 2+2*2+2를 만들 수 있다. 하지만, (2+2*2)+2와 2+(2*2+2)는 만들 수 없다. 그 이유는 쌍이 되지 않는 괄호를 제거했기 때문이다.

어떤 식을 여러 쌍의 괄호가 감쌀 수 있다.

<br/>

## 입력

첫째 줄에 음이 아닌 정수로 이루어진 수식이 주어진다. 이 수식은 괄호가 올바르게 쳐져있다. 숫자, '+', '*', '-', '/', '(', ')'로만 이루어져 있다. 수식의 길이는 최대 200이고, 괄호 쌍은 적어도 1개, 많아야 10개이다. 

<br/>

## 출력

올바른 괄호 쌍을 제거해서 나올 수 있는 서로 다른 식을 사전 순으로 출력한다.

<br/>

## 예제 입력 1

```
(0/(0))
```

## 예제 출력 1

```
(0/0)
0/(0)
0/0
```

## 예제 입력 2

```
(2+(2*2)+2)
```

## 예제 출력 2

```
(2+2*2+2)
2+(2*2)+2
2+2*2+2
```

## 예제 입력 3

```
(1+(2*(3+4)))
```

## 예제 출력 3

```
(1+(2*3+4))
(1+2*(3+4))
(1+2*3+4)
1+(2*(3+4))
1+(2*3+4)
1+2*(3+4)
1+2*3+4
```





### Sol

수식이 주어질 때, 제거 가능한 괄호쌍의 경우의 수를 묻는 문제입니다. 

이처럼 괄호를 대상으로 어떤 처리를 하는 문제들을 종종 만나볼 수 있는데, 그 접근법을 연습하기 좋은 문제인 듯 합니다. 괄호를 대상으로 하는 예시 문제는  다음 2개가 당장 떠오르네요.

[프로그래머스-괄호 변환 - 카카오 블라인드](https://programmers.co.kr/learn/courses/30/lessons/60058)

[프로그래머스-올바른 괄호](https://programmers.co.kr/learn/courses/30/lessons/12909)

<br/>

저는 이 문제를 다음과 같은 단계로 풀이했습니다.

1. 입력 수식을 탐색하며 쌍이 되는 '(' 와 ')'의 위치(idx)를 candidates 리스트로 생성했습니다.
   - 이때, 쌍이 되는지 여부는 Stack을 활용하는데요, 아래 이미지에 입력 예시를 순회하며 어떤 식으로 stack과 candidates가 변해가는지 확인해 보세요.

![image](C:\Program Files\Typora\2021-07-13-[BJ] Removing Bracket\[BJ] Removing Bracket_1.png)

<br/>

2. 이제 생성된 candidates를 활용하여 조합 가능한 경우의 수 만큼 해당 idx 위치의 char를 제거해 answer 리스트에 추가해 줍니다.
   - 조합 가능한 경우의 수는, 1개의 후보를 제거하는 경우 부터 len(candidates) 개(모두 제거) 제거하는 경우까지 존재하겠죠?
   - itertools의 combinations()를 활용합니다.
3. 마지막으로, answer를 사전순 정렬해 주고, 정답을 출력해 주면 끝!

![image](C:\Program Files\Typora\2021-07-13-[BJ] Removing Bracket\[BJ] Removing Bracket_2.png)

<br/>

실제 코드는 다음과 같습니다.



### Code

```python
import itertools
# 0. 입력
A = list(input())
answer = []
# 1.쌍이 되는 '(' 와 ')' 의 위치들을 후보군 리스트로 만듬
candidates = []
idx, stack = 0, []
while idx < len(A):
    if A[idx] == '(':
        stack.append(idx)
    elif A[idx] == ')':
        candidates.append([stack.pop(-1),idx])
    idx += 1

# 2. 조합 가능한 경우만큼 해당 위치를 제거한 answer들을 선정
idxs = [_ for _ in range(len(candidates))]
for n in range(1, len(candidates)+1):
    mycombination = itertools.combinations(idxs, n) # 조합 생성
    for mycomb in mycombination:
        del_list = []
        for _ in mycomb:
            del_list += candidates[_] # 출력하지 않을 index들 선정
        ans = ''
        for _ in range(len(A)):
            if _ not in del_list:
                ans += A[_]
        if ans not in answer: # 중복제거
            answer.append(ans)

answer.sort() # 사전순 정렬
for ans in answer:
    print(ans)


'''
(2+(2*2)+2)
(1+(2*(3+4)))
'''
```

