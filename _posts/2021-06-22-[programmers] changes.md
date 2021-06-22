---
layout: posts
title:  "[프로그래머스] 거스름돈"
categories: ['Algorithm', '프로그래머스']
---

### [프로그래머스] 거스름돈 
[문제링크]:https://programmers.co.kr/learn/courses/30/lessons/12907



#### 문제 설명

Finn은 편의점에서 야간 아르바이트를 하고 있습니다. 야간에 손님이 너무 없어 심심한 Finn은 손님들께 거스름돈을 n 원을 줄 때 방법의 경우의 수를 구하기로 하였습니다.

예를 들어서 손님께 5원을 거슬러 줘야 하고 1원, 2원, 5원이 있다면 다음과 같이 4가지 방법으로 5원을 거슬러 줄 수 있습니다.

- 1원을 5개 사용해서 거슬러 준다.
- 1원을 3개 사용하고, 2원을 1개 사용해서 거슬러 준다.
- 1원을 1개 사용하고, 2원을 2개 사용해서 거슬러 준다.
- 5원을 1개 사용해서 거슬러 준다.

거슬러 줘야 하는 금액 n과 Finn이 현재 보유하고 있는 돈의 종류 money가 매개변수로 주어질 때, Finn이 n 원을 거슬러 줄 방법의 수를 return 하도록 solution 함수를 완성해 주세요.

##### 제한 사항

- n은 100,000 이하의 자연수입니다.
- 화폐 단위는 100종류 이하입니다.
- 모든 화폐는 무한하게 있다고 가정합니다.
- 정답이 커질 수 있으니, 1,000,000,007로 나눈 나머지를 return 해주세요.



##### 입출력 예

| n    | money   | result |
| ---- | ------- | ------ |
| 5    | [1,2,5] | 4      |







#### Sol

DP를 연습하기 좋은 문제입니다.

이 문제를 접근하는데 어려움이 있다면, 유사한 쉬운 문제로 'Climbing Stairs'와 '2 x n 타일링' 을 먼저 풀어보세요.

[Climbing Stairs]: https://leetcode.com/problems/climbing-stairs/
[2 x n 타일링]: https://programmers.co.kr/learn/courses/30/lessons/12900





위 두 문제와 마찬가지로 DP 접근하는 기본적인 아이디어는, 어떤것이 변화했는가에 초점을 맞춥니다.

dp 테이블을 다음과 같이 잡았습니다.

 <img src="https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5Bprogrammers%5D%20change_1.png?raw=true" alt="image-20210622153052430" style="zoom: 33%;" /> <img src="imgs/[programmers] change_2.png" alt="image-20210622153119369" style="zoom:33%;" />
 

가로 축은 '만들고자 하는 값'이며 세로 축은 사용가능한 돈 입니다.

dp테이블의 size는 len(money) * n으로 잡았습니다.





<img src="imgs/[programmers] change_3.png" alt="image-20210622153332409" style="zoom:50%;" />

먼저 0원을 만드는 방법은 공집합이니 1로 채워 줍니다.

그리고 1원만 사용 가능한 경우, target 값이 얼마든 만드는 방법은 1가지 입니다.





<img src="imgs/[programmers] change_4.png" alt="image-20210622153623270" style="zoom:50%;" />

2원도 사용이 가능해진 두번째 행을 채워 봅시다.

target이 2원일 때, 경우의수가 2가지 경우의 합으로 볼 수 있습니다. 

​	1) 2원을 사용하지 않고 1원만 사용해 2원을 만드는 방법의 수

​	2) 2원을 사용하는 경우의 target - 2 원을 만드는 방법의 수





아직 잘 감이 안온다면, 좀 더 살펴봅시다.

<img src="imgs/[programmers] change_5.png" alt="image-20210622154039989" style="zoom:50%;" />

target이 5원이라면, 어떤 경우의 수가 있을까요?

[1,1,1,1,1], [1,1,1,2], [1,2,2] 의 3가지 경우가 있을 것 이며 이것은,

​	1) 2원을 사용하지 않고 1원만 사용해 5원을 만드는 방법의 수

​	2) 2원을 사용하는 경우 target - 2인  3원을 만드는 방법의 수

의 합인 것을 확인할 수 있습니다.





<img src="imgs/[programmers] change_6.png" alt="image-20210622154344025" style="zoom:50%;" />

결국, dp[i] [j] = dp[i-1] [j] + dp[i] [j - money[i]] 라는 일반항을 구할 수 있습니다. 

최종적으로는 return dp[-1] [-1] 을 반환하게 됩니다.







#### Code

```python
def solution(n, money):
    dp = [([1] + [0] * n) for _ in range(len(money))]
    
    # dp[i][j] = dp[i-1][j] + dp[i][j-money[i]]
    for i in range(len(money)):
        for j in range(1, len(dp[0])): 
            if i == 0: # dp[i-1]이 없는 경우
                dp[i][j] = dp[i][j-money[i]]
            else:
                dp[i][j] = dp[i-1][j] + dp[i][j-money[i]]
    
    return dp[-1][-1]

```



