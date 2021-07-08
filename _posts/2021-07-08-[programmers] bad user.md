---
layout: posts
title:  "[프로그래머스] 불량 사용자"
categories: ['Algorithm', '프로그래머스']
---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/64064)
<br/>



###### 문제 설명

개발팀 내에서 이벤트 개발을 담당하고 있는 "무지"는 최근 진행된 카카오이모티콘 이벤트에 비정상적인 방법으로 당첨을 시도한 응모자들을 발견하였습니다. 이런 응모자들을 따로 모아 `불량 사용자`라는 이름으로 목록을 만들어서 당첨 처리 시 제외하도록 이벤트 당첨자 담당자인 "프로도" 에게 전달하려고 합니다. 이 때 개인정보 보호을 위해 사용자 아이디 중 일부 문자를 '*' 문자로 가려서 전달했습니다. 가리고자 하는 문자 하나에 '*' 문자 하나를 사용하였고 아이디 당 최소 하나 이상의 '*' 문자를 사용하였습니다.
"무지"와 "프로도"는 불량 사용자 목록에 매핑된 응모자 아이디를 `제재 아이디` 라고 부르기로 하였습니다.

예를 들어, 이벤트에 응모한 전체 사용자 아이디 목록이 다음과 같다면

| 응모자 아이디 |
| ------------- |
| frodo         |
| fradi         |
| crodo         |
| abc123        |
| frodoc        |

다음과 같이 불량 사용자 아이디 목록이 전달된 경우,

| 불량 사용자 |
| ----------- |
| fr*d*       |
| abc1**      |

불량 사용자에 매핑되어 당첨에서 제외되어야 야 할 제재 아이디 목록은 다음과 같이 두 가지 경우가 있을 수 있습니다.

| 제재 아이디 |
| ----------- |
| frodo       |
| abc123      |

| 제재 아이디 |
| ----------- |
| fradi       |
| abc123      |

이벤트 응모자 아이디 목록이 담긴 배열 user_id와 불량 사용자 아이디 목록이 담긴 배열 banned_id가 매개변수로 주어질 때, 당첨에서 제외되어야 할 제재 아이디 목록은 몇가지 경우의 수가 가능한 지 return 하도록 solution 함수를 완성해주세요.

#### **[제한사항]**

- user_id 배열의 크기는 1 이상 8 이하입니다.
- user_id 배열 각 원소들의 값은 길이가 1 이상 8 이하인 문자열입니다.
  - 응모한 사용자 아이디들은 서로 중복되지 않습니다.
  - 응모한 사용자 아이디는 알파벳 소문자와 숫자로만으로 구성되어 있습니다.
- banned_id 배열의 크기는 1 이상 user_id 배열의 크기 이하입니다.
- banned_id 배열 각 원소들의 값은 길이가 1 이상 8 이하인 문자열입니다.
  - 불량 사용자 아이디는 알파벳 소문자와 숫자, 가리기 위한 문자 '*' 로만 이루어져 있습니다.
  - 불량 사용자 아이디는 '*' 문자를 하나 이상 포함하고 있습니다.
  - 불량 사용자 아이디 하나는 응모자 아이디 중 하나에 해당하고 같은 응모자 아이디가 중복해서 제재 아이디 목록에 들어가는 경우는 없습니다.
- 제재 아이디 목록들을 구했을 때 아이디들이 나열된 순서와 관계없이 아이디 목록의 내용이 동일하다면 같은 것으로 처리하여 하나로 세면 됩니다.

------

##### **[입출력 예]**

| user_id                                           | banned_id                                | result |
| ------------------------------------------------- | ---------------------------------------- | ------ |
| `["frodo", "fradi", "crodo", "abc123", "frodoc"]` | `["fr*d*", "abc1**"]`                    | 2      |
| `["frodo", "fradi", "crodo", "abc123", "frodoc"]` | `["*rodo", "*rodo", "******"]`           | 2      |
| `["frodo", "fradi", "crodo", "abc123", "frodoc"]` | `["fr*d*", "*rodo", "******", "******"]` | 3      |

##### **입출력 예에 대한 설명**

##### **입출력 예 #1**

문제 설명과 같습니다.

##### **입출력 예 #2**

다음과 같이 두 가지 경우가 있습니다.

| 제재 아이디 |
| ----------- |
| frodo       |
| crodo       |
| abc123      |

| 제재 아이디 |
| ----------- |
| frodo       |
| crodo       |
| frodoc      |

##### **입출력 예 #3**

다음과 같이 세 가지 경우가 있습니다.

| 제재 아이디 |
| ----------- |
| frodo       |
| crodo       |
| abc123      |
| frodoc      |

| 제재 아이디 |
| ----------- |
| fradi       |
| crodo       |
| abc123      |
| frodoc      |

| 제재 아이디 |
| ----------- |
| fradi       |
| frodo       |
| abc123      |
| frodoc      |



<br/>



### Sol

카카오 코딩테스트 문제치고는 상당히 쉽게 해결되는 문제였습니다.

최근 일주일정도 일이 몰려서 알고리즘을 못 풀고 지내다가 오랜만에 워밍업(?) 하기 좋은 문제였습니다.

제가 접근한 풀이의 핵심은 '순열'을 활용한 경우의 수 탐색 방법이었습니다.

<br/>

1. 먼저 board를 만들어 주었습니다. 사용자 목록과 불량 사용자명이 매핑이 되는지 여부를 판단하였습니다.

   (글씨가 많이 날라가네요 머쓱ㅎㅎㅎ)

   ![image-20210709003603185](C:\Program Files\Typora\2021-0708-[programmers] bad user\image-20210709003603185.png)



2. python에서 제가 애정하는 패키지 itertools를 활용해 permutation(순열) 을 생성해 줍니다.

   ![image-20210709003937727](C:\Program Files\Typora\2021-0708-[programmers] bad user\image-20210709003937727.png)

3. 이제 board를 참조하며 

   ```python
   board[_][myperm[_]]
   ```

   이 모두 1인(가능한) 경우의 수를 모두 answer에 append() 해줍니다.

4. answer에서 중복을 제거한 후, len(answer)를 반환해 주면 해결!



<br/>

### Code

```python
import itertools
def candi_checker(id1, id2):  # (banned_id, user_id)
    if len(id1) != len(id2):
        return 0
    idx = 0
    while idx < len(id1):
        if id1[idx] != '*' and id1[idx] != id2[idx]:
            return 0
        idx += 1
    return 1


def solution(user_id, banned_id):
    answer = []
    idxs = [_ for _ in range(len(user_id))]
    # make board
    board = [[0 for j in range(len(user_id))] for i in range(len(banned_id))]
    for i in range(len(banned_id)):
        for j in range(len(user_id)):
            board[i][j] = candi_checker(banned_id[i], user_id[j])

    mypermutation = itertools.permutations(idxs,len(banned_id))
    for myperm in mypermutation:
        cnt = len(banned_id)
        for _ in range(len(banned_id)):
            if board[_][myperm[_]] == 1:
                cnt -= 1
                if cnt == 0:
                    answer.append(myperm)
            else:
                break

    answer = len(list(set([tuple(set(ans)) for ans in answer])))
    return answer
```

