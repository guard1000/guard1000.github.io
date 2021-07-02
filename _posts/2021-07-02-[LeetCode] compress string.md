---
layout: posts
title:  "[프로그래머스] 문자열 압축"
categories: ['Algorithm', '프로그래머스']


---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/60057)

<br/>

###### 문제 설명

데이터 처리 전문가가 되고 싶은 **"어피치"**는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.
간단한 예로 "aabbaccc"의 경우 "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, "abcabcdede"와 같은 문자열은 전혀 압축되지 않습니다. "어피치"는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, "ababcdcdababcdcd"의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 "2ab2cd2ab2cd"로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 "2ababcdcd"로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, "abcabcdede"와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 "abcabc2de"가 되지만, 3개 단위로 자른다면 "2abcdede"가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- s의 길이는 1 이상 1,000 이하입니다.
- s는 알파벳 소문자로만 이루어져 있습니다.

##### 입출력 예

| s                            | result |
| ---------------------------- | ------ |
| `"aabbaccc"`                 | 7      |
| `"ababcdcdababcdcd"`         | 9      |
| `"abcabcdede"`               | 8      |
| `"abcabcabcabcdededededede"` | 14     |
| `"xababcdcdababcdcd"`        | 17     |

### 입출력 예에 대한 설명

**입출력 예 #1**

문자열을 1개 단위로 잘라 압축했을 때 가장 짧습니다.

**입출력 예 #2**

문자열을 8개 단위로 잘라 압축했을 때 가장 짧습니다.

**입출력 예 #3**

문자열을 3개 단위로 잘라 압축했을 때 가장 짧습니다.

**입출력 예 #4**

문자열을 2개 단위로 자르면 "abcabcabcabc6de" 가 됩니다.
문자열을 3개 단위로 자르면 "4abcdededededede" 가 됩니다.
문자열을 4개 단위로 자르면 "abcabcabcabc3dede" 가 됩니다.
문자열을 6개 단위로 자를 경우 "2abcabc2dedede"가 되며, 이때의 길이가 14로 가장 짧습니다.

**입출력 예 #5**

문자열은 제일 앞부터 정해진 길이만큼 잘라야 합니다.
따라서 주어진 문자열을 x / ababcdcd / ababcdcd 로 자르는 것은 불가능 합니다.
이 경우 어떻게 문자열을 잘라도 압축되지 않으므로 가장 짧은 길이는 17이 됩니다.



<br/>

### Sol

문자열을 요리조리 다뤄보는 문제입니다.

보통 카카오 코테에서 다루는 수준보다는 쉬운 난이도로, 아마 1번문제 정도였을 듯 합니다.

제가 카카오에 근무할 때 위 문제와 유사하게 '비손실압축과 복원'을 어떻게 효과적으로 할 것인가에 대한

프로젝트를 진행했었는데요(이미지 분야였지만, 결국 다 비슷하죠 뭐). 그래서 이 문제를 보니 반가운 마음에 끄적여 봅니다.

<br/>

#### 1. 저는 counter라는 function을 하나 만들었습니다. 이녀석은 문자열 s와 몇글자씩 나눌지인 n을 입력받습니다.

![image-20210702161409458](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5Bprogrammers%5D%20compress%20string_1.png?raw=true)



#### 2. 먼저, 입력받은 s를 위 그림처럼 n에 따라 분할해 주어야겠죠?

   다음과 같이 가볍게 슬라이싱으로 처리해 줍시다.

   ```python
   s = [s[i:i+n] for i in range(0, len(s), n)]
   ```

<br/>

![image-20210702161637880](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5Bprogrammers%5D%20compress%20string_2.png?raw=true)

#### 3. 이어서 while문을 통해 각 문자별 반복횟수를 정의하는 dictionary를 생성해 줍니다.

   위 그림의 예시는 n=1인 경우 idx별로 dic이 어떻게 변화하는지 확인할 수 있습니다.

   <br/>

#### 4. 생성된 dictionary를 토대로 압축된 문자열의 길이가 얼마인지를 구해줍니다.

   3-1)은 key들의 문자 부분에 대한 값을 구하는 부분이며

   3-2)는 문자열 앞에 숫자가 차지할 길이를 구해주는 부분입니다.

   <br/>

#### 5. 이제 1~3에서 정의한 counter함수를 활용해 입력된 s에 n 값을 달리하며 가장 반환된 길이가 짧은 것을 answer로 반환하면 됩니다.

   이때, n은 len(s)의 절반까지만 확인해도 됩니다!



<br/>

### Code

```python
def counter(s, n):
    s = [s[i:i+n] for i in range(0, len(s), n)]
    idx, tmp_val, tmp_cnt, dic = 0, '', 0, {}
    while idx < len(s):
        if s[idx] != tmp_val:
            key = str(idx) + '_' + s[idx]
            dic[key] = 1
            tmp_val = s[idx]
            tmp_cnt = 1
        else:
            key = str(idx-tmp_cnt) + '_' + s[idx]
            dic[key] += 1
            tmp_cnt += 1
        idx += 1
    
    countval = 0
    for key in dic:
        countval += len(key.split('_')[-1])
        if dic[key] != 1:
            countval += len(str(dic[key]))
            
    return countval
    
    
def solution(s):
    if len(s) == 1:
        return 1
    
    answer = 1000
    for n in range(1,len(s)//2 + 1):
        ans = counter(s, n)
        if ans < answer:
            answer = ans
    
    return answer
```



