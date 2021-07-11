---
layout: posts
title:  "[프로그래머스] 거리두기 확인하기"
categories: ['Algorithm', '프로그래머스']

---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/81302)
<br/>



###### 문제 설명

개발자를 희망하는 죠르디가 카카오에 면접을 보러 왔습니다.

코로나 바이러스 감염 예방을 위해 응시자들은 거리를 둬서 대기를 해야하는데 개발 직군 면접인 만큼
아래와 같은 규칙으로 대기실에 거리를 두고 앉도록 안내하고 있습니다.

> 1. 대기실은 5개이며, 각 대기실은 5x5 크기입니다.
> 2. 거리두기를 위하여 응시자들 끼리는 맨해튼 거리[1](https://programmers.co.kr/learn/courses/30/lessons/81302#fn1)가 2 이하로 앉지 말아 주세요.
> 3. 단 응시자가 앉아있는 자리 사이가 파티션으로 막혀 있을 경우에는 허용합니다.

예를 들어,

| ![PXP.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8c056cac-ec8f-435c-a49a-8125df055c5e/PXP.png | ![PX_XP.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/d611f66e-f9c4-4433-91ce-02887657fe7f/PX_XP.png) | ![PX_OP.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/ed707158-0511-457b-9e1a-7dbf34a776a5/PX_OP.png) |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 위 그림처럼 자리 사이에 파티션이 존재한다면 맨해튼 거리가 2여도 거리두기를 **지킨 것입니다.** | 위 그림처럼 파티션을 사이에 두고 앉은 경우도 거리두기를 **지킨 것입니다.** | 위 그림처럼 자리 사이가 맨해튼 거리 2이고 사이에 빈 테이블이 있는 경우는 거리두기를 **지키지 않은 것입니다.** |
| ![P.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4c548421-1c32-4947-af9e-a45c61501bc4/P.png) | ![O.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/ce799a38-668a-4038-b32f-c515b8701262/O.png) | ![X.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/91e8f98b-baeb-4f81-8cb6-5bafebebdcc7/X.png) |
|          응시자가 앉아있는 자리(`P`)를 의미합니다.           |                 빈 테이블(`O`)을 의미합니다.                 |                  파티션(`X`)을 의미합니다.                   |

5개의 대기실을 본 죠르디는 각 대기실에서 응시자들이 거리두기를 잘 기키고 있는지 알고 싶어졌습니다. 자리에 앉아있는 응시자들의 정보와 대기실 구조를 대기실별로 담은 2차원 문자열 배열 `places`가 매개변수로 주어집니다. 각 대기실별로 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

------

##### 제한사항

- `places`의 행 길이(대기실 개수) = 5
- - `places`의 각 행은 하나의 대기실 구조를 나타냅니다.
- `places`의 열 길이(대기실 세로 길이) = 5
- `places`의 원소는 `P`,`O`,`X`로 이루어진 문자열입니다.
- - `places` 원소의 길이(대기실 가로 길이) = 5
  - `P`는 응시자가 앉아있는 자리를 의미합니다.
  - `O`는 빈 테이블을 의미합니다.
  - `X`는 파티션을 의미합니다.
- 입력으로 주어지는 5개 대기실의 크기는 모두 5x5 입니다.
- return 값 형식
  - 1차원 정수 배열에 5개의 원소를 담아서 return 합니다.
  - `places`에 담겨 있는 5개 대기실의 순서대로, 거리두기 준수 여부를 차례대로 배열에 담습니다.
  - 각 대기실 별로 모든 응시자가 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 담습니다.



------

##### 입출력 예

| places                                                       | result          |
| ------------------------------------------------------------ | --------------- |
| `[["POOOP", "OXXOX", "OPXPX", "OOXOX", "POXXP"], ["POOPX", "OXPXP", "PXXXO", "OXXXO", "OOOPP"], ["PXOPX", "OXOXP", "OXPOX", "OXXOP", "PXPOX"], ["OOOXX", "XOOOX", "OOOXX", "OXOOX", "OOOOO"], ["PXPXP", "XPXPX", "PXPXP", "XPXPX", "PXPXP"]]` | [1, 0, 1, 1, 1] |

------

##### 입출력 예 설명

**입출력 예 #1**

첫 번째 대기실

|      |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| No.  | 0    | 1    | 2    | 3    | 4    |
| 0    | P    | O    | O    | O    | P    |
| 1    | O    | X    | X    | O    | X    |
| 2    | O    | P    | X    | P    | X    |
| 3    | O    | O    | X    | O    | X    |
| 4    | P    | O    | X    | X    | P    |

- 모든 응시자가 거리두기를 지키고 있습니다.

두 번째 대기실

|      |       |      |       |       |       |
| ---- | ----- | ---- | ----- | ----- | ----- |
| No.  | 0     | 1    | 2     | 3     | 4     |
| 0    | **P** | O    | O     | **P** | X     |
| 1    | O     | X    | **P** | X     | P     |
| 2    | **P** | X    | X     | X     | O     |
| 3    | O     | X    | X     | X     | O     |
| 4    | O     | O    | O     | **P** | **P** |

- (0, 0) 자리의 응시자와 (2, 0) 자리의 응시자가 거리두기를 지키고 있지 않습니다.
- (1, 2) 자리의 응시자와 (0, 3) 자리의 응시자가 거리두기를 지키고 있지 않습니다.
- (4, 3) 자리의 응시자와 (4, 4) 자리의 응시자가 거리두기를 지키고 있지 않습니다.

세 번째 대기실

|      |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| No.  | 0    | 1    | 2    | 3    | 4    |
| 0    | P    | X    | O    | P    | X    |
| 1    | O    | X    | O    | X    | P    |
| 2    | O    | X    | P    | O    | X    |
| 3    | O    | X    | X    | O    | P    |
| 4    | P    | X    | P    | O    | X    |

- 모든 응시자가 거리두기를 지키고 있습니다.

네 번째 대기실

|      |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| No.  | 0    | 1    | 2    | 3    | 4    |
| 0    | O    | O    | O    | X    | X    |
| 1    | X    | O    | O    | O    | X    |
| 2    | O    | O    | O    | X    | X    |
| 3    | O    | X    | O    | O    | X    |
| 4    | O    | O    | O    | O    | O    |

- 대기실에 응시자가 없으므로 거리두기를 지키고 있습니다.

다섯 번째 대기실

|      |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| No.  | 0    | 1    | 2    | 3    | 4    |
| 0    | P    | X    | P    | X    | P    |
| 1    | X    | P    | X    | P    | X    |
| 2    | P    | X    | P    | X    | P    |
| 3    | X    | P    | X    | P    | X    |
| 4    | P    | X    | P    | X    | P    |

- 모든 응시자가 거리두기를 지키고 있습니다.

두 번째 대기실을 제외한 모든 대기실에서 거리두기가 지켜지고 있으므로, 배열 [1, 0, 1, 1, 1]을 return 합니다.

------

##### 제한시간 안내

- 정확성 테스트 : 10초

------

1. 두 테이블 T1, T2가 행렬 (r1, c1), (r2, c2)에 각각 위치하고 있다면, T1, T2 사이의 맨해튼 거리는 |r1 - r2| + |c1 - c2| 입니다. 



<br/>

### Sol

따끈따끈한 2021 카카오 채용연계 인턴십 문제입니다.

카카오 코테치고 난이도는 어렵지 않은것으로 보아 1번이나 2번 문제였을 것으로 생각드네요!

특별히 알고리즘적인 기발한 인사이트가 필요하진 않고, 경우의 수 역시 5*5맵이라는 지정된 사이즈의 맵에서 발생하는 것이므로, 효율성을 크게 고려하지 않아도 될 것으로 생각이 듭니다.

옛날 제 경험으로는 삼성 SW 자격시험 A형 문제가 이 정도 수준이었던 것 같습니다. (구현 위주, 효율성보단 정확성 위주)

<br/>

저는 풀이를 다음과 같은 순서로 진행했습니다.

1.  place별로 'P'(사람) 들의 위치를 people 리스트로 추출

2. people의 각 사람별 맨해튼거리 2 이하에 위치한 'P'들을 위치를 candidates 리스트로 추출

3. candidates 내 후보자들을 대상으로 다음 조건별 거리두기 여부를 확인

   -  candidate과 person이 같은 행에 존재하는 경우

     - x좌표 차이가 1인 경우 -> 바로 옆이므로 거리두기 X
     - 두 칸 떨어져 있는 경우엔, person과 candidate의 x좌표 평균값(가운데 값)이 'O'(테이블) 인 경우 -> 거리두가 X

   - candidate과 person이 같은 열에 존재하는 경우

     - y좌표 차이가 1인 경우 -> 바로 옆이므로 거리두기 X
     - 두 칸 떨어져 있는 경우엔, person과 candidate의 y좌표 평균값(가운데 값)이 'O'(테이블) 인 경우 -> 거리두기 X

   - candidate와 person이 행/열이 다른 위치인 경우 - 대각에 위치

     - candidate와 person의 y, x 좌표 각각의 min 값을 y_min과 x_min이라 가정할 때,

       place의 다음 네 좌표 (y_min, x_min), (y_min+1, x_min), (y_min, x_min+1), (y_min+1, x_min+1)  중엔 'O'가 존재할 경우 -> 거리두기 X

       -> 대각인 경우 P 2개와 X 2개가 교차된 경우만 거리두기이기 때문!

<br/>

위 풀이과정 1~3을 코드로 작성하면 아래와 같습니다.



### Code

```python
def solution(places):
    answer = []
    # 1. place에서 'P'(사람) 들만 추출
    for place in places:
        people = []
        for y in range(5):
            for x in range(5):
                if place[y][x] == 'P':
                    people.append([y,x])
        
        tmp = 1
        # 2. 각 사람별 맨해튼거리 2 이하에 위치한 'P'들 - candidates 추출
        for person in people:
            candidates = []
            for y in range(person[0]-2, person[0]+3):
                for x in range(person[1]-2, person[1]+3):
                    if (-1 < x < 5) and (-1 < y < 5) and (abs(y-person[0]) + abs(x-person[1])) <= 2 and place[y][x] == 'P' and not (y == person[0] and x == person[1]):
                        candidates.append([y,x])
            
            y, x = person[0], person[1] # person의 위치정보를 [y,x]로 저장
            
            # 3. 후보자들 대상으로 다음 조건별 거리두기 확인
            #  1) candidates 중 행 같은 경우
            #  2) candidates 중 열 같은 경우
            #  3) candidates 중 행,열 다른 경우(대각)
            for candi in candidates:
                if candi[0] == y: # 같은 행에 있을 경우
                    if abs(x-candi[1]) == 1:    # 바로 옆인 경우 -> 거리두기 X
                        tmp = 0
                        break
                    if place[y][(x+candi[1])//2] == 'O':   #  두 칸 떨어져 있는경우, 가운데 'O'인지 확인
                        tmp = 0
                        break
                        
                elif candi[1] == x: # 같은 열에 있을 경우
                    if abs(y-candi[0]) == 1:    # 바로 위아래인 경우 -> 거리두기 X
                        tmp = 0
                        break
                    if place[(y+candi[0])//2][x] == 'O':   #  두 칸 떨어져 있는경우, 가운데 'O'인지 확인
                        tmp = 0
                        break                             
                else:   # 대각에 위치한 경우, 그 사이에 'O'가 존재하면 거리두기 X
                    y_min, x_min = min(candi[0], y), min(candi[1], x)
                    if 'O' in [place[y_min][x_min], place[y_min+1][x_min], place[y_min][x_min+1], place[y_min+1][x_min+1]]:
                        tmp = 0
                        break
            
            if tmp == 0:    # candidates 거리두기 확인 중 1건이라도 실패시 break
                break
            
        answer.append(tmp)
    
    return answer
```















