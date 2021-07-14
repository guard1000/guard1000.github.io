---
layout: posts
title:  "[프로그래머스] 기지국 설치"
categories: ['Algorithm', '프로그래머스']

---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/12979)
<br/>



###### 문제 설명

N개의 아파트가 일렬로 쭉 늘어서 있습니다. 이 중에서 일부 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 기술이 발전해 5g 수요가 높아져 4g 기지국을 5g 기지국으로 바꾸려 합니다. 그런데 5g 기지국은 4g 기지국보다 전달 범위가 좁아, 4g 기지국을 5g 기지국으로 바꾸면 어떤 아파트에는 전파가 도달하지 않습니다.

예를 들어 11개의 아파트가 쭉 늘어서 있고, [4, 11] 번째 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 만약 이 4g 기지국이 전파 도달 거리가 1인 5g 기지국으로 바뀔 경우 모든 아파트에 전파를 전달할 수 없습니다. (전파의 도달 거리가 W일 땐, 기지국이 설치된 아파트를 기준으로 전파를 양쪽으로 W만큼 전달할 수 있습니다.)

- 초기에, 1, 2, 6, 7, 8, 9번째 아파트에는 전파가 전달되지 않습니다.

![기지국설치1_pvskxt.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/fcb45e06-ebb2-4d93-98cc-b6203185e933/%E1%84%80%E1%85%B5%E1%84%8C%E1%85%B5%E1%84%80%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B51_pvskxt.png)

- 1, 7, 9번째 아파트 옥상에 기지국을 설치할 경우, 모든 아파트에 전파를 전달할 수 있습니다.

![기지국설치2_kml0pb.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/dd31ddb8-f50d-404c-a6f5-8d6a1d88f620/%E1%84%80%E1%85%B5%E1%84%8C%E1%85%B5%E1%84%80%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B52_kml0pb.png)

- 3개의 아파트보다 더 많은 아파트 옥상에 기지국을 설치할 경우에도 모든 아파트에 전파를 전달할 수 있습니다.

![기지국설치3_xhv7r3.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/f5801b12-f683-422d-b26f-5e23e72915dc/%E1%84%80%E1%85%B5%E1%84%8C%E1%85%B5%E1%84%80%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B53_xhv7r3.png)

이때, 우리는 기지국을 **최소로 설치**하면서 모든 아파트에 전파를 전달하려고 합니다. 위의 예시에선 최소 3개의 아파트 옥상에 기지국을 설치해야 모든 아파트에 전파를 전달할 수 있습니다.

아파트의 개수 N, 현재 기지국이 설치된 아파트의 번호가 담긴 1차원 배열 stations, 전파의 도달 거리 W가 매개변수로 주어질 때, 모든 아파트에 전파를 전달하기 위해 증설해야 할 기지국 개수의 최솟값을 리턴하는 solution 함수를 완성해주세요

##### 제한사항

- N: 200,000,000 이하의 자연수
- stations의 크기: 10,000 이하의 자연수
- stations는 오름차순으로 정렬되어 있고, 배열에 담긴 수는 N보다 같거나 작은 자연수입니다.
- W: 10,000 이하의 자연수

------

##### 입출력 예

| N    | stations | W    | answer |
| ---- | -------- | ---- | ------ |
| 11   | [4, 11]  | 1    | 3      |
| 16   | [9]      | 2    | 3      |

##### 입출력 예 설명

입출력 예 #1
문제의 예시와 같습니다

입출력 예 #2

- 초기에, 1-6, 12-16번째 아파트에는 전파가 전달되지 않습니다.

![기지국설치4_nqfrmm.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/1d766102-f684-4643-bea2-02daea82e710/%E1%84%80%E1%85%B5%E1%84%8C%E1%85%B5%E1%84%80%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B54_nqfrmm.png)

- 3, 6, 14번째 아파트 옥상에 기지국을 설치할 경우 모든 아파트에 전파를 전달할 수 있습니다.

![기지국설치5_zh4ebk.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/bc7d4fdb-cb48-4f45-b2eb-977cfb2c54dd/%E1%84%80%E1%85%B5%E1%84%8C%E1%85%B5%E1%84%80%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B55_zh4ebk.png)



<br/>

### Sol

통신사에 근무중인 제게 흥미로운 문제여서 클릭해 버렸습니다ㅋㅋㅋㅋ

물론 5G 기지국 설치에 대한 로직을 이렇게 단순히 할 순 없겠지만... 이러한 최적화 문제는 현업에서도 다양한 로직을 개발하고 고민하고 계신걸로 압니다. ㅎㅎ

<br/>

입력 N의 범위를 보아하니, 얼마나 효율적으로 푸느냐가 중요할 것 같습니다. 

저는 station들이 오름차순으로 정렬이 이미 되어 있다는 점에서 다음과 같은 룰을 세웠습니다.

지금 위치를 pos 라고 잡았을 때,

1. station 범위 밖의 왼쪽에 pos가 위치해 있는 경우 or 가장 큰 station의 범위 밖 오른쪽에 있는 경우

   -> 기지국을 새로 설치해야 합니다.

   -> answer += 1 해주고, 새로 설치한 기지국의 범위 +1 로 pos를 옮겨 줍니다.

   -> pos += (2*w+1)

2. 현재 station의 범위 안에 pos가 위치한 경우

   -> pos를 현재 station 범위 +1 로 이동

3. station 범위 밖 오른쪽에 위치하는 경우

   -> 다음 station을 대상으로 가리킵니다.

   -> station_idx += 1



![image](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5Bprogrammers%5D%20station_1.png?raw=true)





<br/>

위 그림과 같이 Rule을 적용하면, 문제에서 주어진 예시상황이 어떻게 전개되는지도 이미지의 오른쪽에서 확인할 수 있습니다. 

이제 이를 코드로 구현하면 다음과 같습니다.



### Code

```python
def solution(n, stations, w):
    answer = 0
    station_idx = 0
    pos = 1
    while pos <= n:
        # station 범위 밖의 왼쪽일 때
        if station_idx == len(stations) or pos < stations[station_idx]-w:
            pos += (2*w + 1)
            answer += 1
        # station 범위 안일 때
        elif stations[station_idx]-w <= pos <= stations[station_idx]+w:
            pos = stations[station_idx]+w+1
            station_idx += 1
        # station 범위 밖의 오른쪽일 때
        elif stations[station_idx]+w < pos:
            station_idx += 1
    
    return answer
```















