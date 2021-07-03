---
layout: posts
title:  "[프로그래머스] 보석쇼핑"
categories: ['Algorithm', 'Programmers']
---

[문제링크](https://leetcode.com/problems/unique-paths/)




[문제링크](https://programmers.co.kr/learn/courses/30/lessons/67258)

<br/>

문제 설명
[본 문제는 정확성과 효율성 테스트 각각 점수가 있는 문제입니다.]

개발자 출신으로 세계 최고의 갑부가 된 어피치는 스트레스를 받을 때면 이를 풀기 위해 오프라인 매장에 쇼핑을 하러 가곤 합니다.
어피치는 쇼핑을 할 때면 매장 진열대의 특정 범위의 물건들을 모두 싹쓸이 구매하는 습관이 있습니다.
어느 날 스트레스를 풀기 위해 보석 매장에 쇼핑을 하러 간 어피치는 이전처럼 진열대의 특정 범위의 보석을 모두 구매하되 특별히 아래 목적을 달성하고 싶었습니다.
진열된 모든 종류의 보석을 적어도 1개 이상 포함하는 가장 짧은 구간을 찾아서 구매

예를 들어 아래 진열대는 4종류의 보석(RUBY, DIA, EMERALD, SAPPHIRE) 8개가 진열된 예시입니다.

진열대 번호	1	2	3	4	5	6	7	8
보석 이름	DIA	RUBY	RUBY	DIA	DIA	EMERALD	SAPPHIRE	DIA
진열대의 3번부터 7번까지 5개의 보석을 구매하면 모든 종류의 보석을 적어도 하나 이상씩 포함하게 됩니다.

진열대의 3, 4, 6, 7번의 보석만 구매하는 것은 중간에 특정 구간(5번)이 빠지게 되므로 어피치의 쇼핑 습관에 맞지 않습니다.

진열대 번호 순서대로 보석들의 이름이 저장된 배열 gems가 매개변수로 주어집니다. 이때 모든 보석을 하나 이상 포함하는 가장 짧은 구간을 찾아서 return 하도록 solution 함수를 완성해주세요.
가장 짧은 구간의 시작 진열대 번호와 끝 진열대 번호를 차례대로 배열에 담아서 return 하도록 하며, 만약 가장 짧은 구간이 여러 개라면 시작 진열대 번호가 가장 작은 구간을 return 합니다.

[제한사항]
gems 배열의 크기는 1 이상 100,000 이하입니다.
gems 배열의 각 원소는 진열대에 나열된 보석을 나타냅니다.
gems 배열에는 1번 진열대부터 진열대 번호 순서대로 보석이름이 차례대로 저장되어 있습니다.
gems 배열의 각 원소는 길이가 1 이상 10 이하인 알파벳 대문자로만 구성된 문자열입니다.
입출력 예
gems	result
["DIA", "RUBY", "RUBY", "DIA", "DIA", "EMERALD", "SAPPHIRE", "DIA"]	[3, 7]
["AA", "AB", "AC", "AA", "AC"]	[1, 3]
["XYZ", "XYZ", "XYZ"]	[1, 1]
["ZZZ", "YYY", "NNNN", "YYY", "BBB"]	[1, 5]
입출력 예에 대한 설명
입출력 예 #1
문제 예시와 같습니다.

입출력 예 #2
3종류의 보석(AA, AB, AC)을 모두 포함하는 가장 짧은 구간은 [1, 3], [2, 4]가 있습니다.
시작 진열대 번호가 더 작은 [1, 3]을 return 해주어야 합니다.

입출력 예 #3
1종류의 보석(XYZ)을 포함하는 가장 짧은 구간은 [1, 1], [2, 2], [3, 3]이 있습니다.
시작 진열대 번호가 가장 작은 [1, 1]을 return 해주어야 합니다.

입출력 예 #4
4종류의 보석(ZZZ, YYY, NNNN, BBB)을 모두 포함하는 구간은 [1, 5]가 유일합니다.
그러므로 [1, 5]를 return 해주어야 합니다.



<br/>

### Sol

최근 Two pointers를 다루는 문제를 몇개 소개했었습니다.
이 문제 역시 Two Pointers로 solution을 작성하여야 효율성 테스트를 무사히 통과하는 문제입니다.
저 역시 처음엔 완전탐색으로 Time Limit에 걸렸었고, 가장 짧은 구간의 길이를 mid값으로 잡아 이진탐색으로도 시도했으나, 역시 테스트 케이스 하나를 통과하지 못했습니다.
항상 카카오 코테에서는 효율성 검증이 들어가는 문제들은 아이디어 싸움이 되는 것 같습니다.
마침 최근에 Two Pointers 문제를 몇몇 다루었던 점이 떠올라서 이 문제를 가져왔습니다.



<br/>

#### 1. 
먼저 Edge 케이스들을 제거했습니다.
주어진 보석의 종류가 한 종류인 경우나, 혹은 모두 다른 종류인 경우에 대해 불필요한 연산을 하지 않게 했습니다.


#### 2. 
이제부터는 Two Pointers입니다.
left와 right를 모두 0으로 초기화 해 주고, 가방(딕셔너리)에 보석을 수집하면서 진행합니다.
<br/>
만약 보석을 아직 다 수집하지 못했다면, 가방에 보석을 추가해주면서 right를 1씩 증가시킵니다.
이미 보석을 종류별로 수집한 상태라면, left를 하나씩 증가시켜가며 보석을 버려봅니다.
이렇게 left부터 right 사이의 공간에서 모든 보석이 존재하는 구간들을 알아낼 수 있고, 이때 최소값을 찾아갈 수 있습니다.
<br/>
특히, 시간복잡도는 O(N)이라는 점이 정말 매력적입니다.
아래 예시를 통해 첫번째 테스트케이스가 어떤 동작으로 답을 반환하게 되는지 함께 이해해 보세요 :)

![image-20210702161637880](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5Bprogrammers%5D%20gems%20shopping_1.png?raw=true?raw=true)



<br/>

### Code

```python
def solution(gems):
    answer = [0,100000]
    N = len(gems)
    n_gems = len(set(gems))
    gems_cnt = {gems[0] : 1}
    
    # edge_case 제거 - 1종류 or N종류
    if n_gems == 1:
        return [1,1]
    if n_gems == N:
        return [1,n_gems]
    
    l,r = 0,0
    while l>-1 and r<N: # boundary check
        if len(gems_cnt) != n_gems : # 다 수집 못 했으면 보석줍줍
            r += 1
            if r == N:
                break
            
            if gems[r] in gems_cnt:
                gems_cnt[gems[r]] += 1
            else:
                gems_cnt[gems[r]] = 1
                    
        else: # 종류별 수집 되어 있으면 l 을 버려봄
            if r-l < answer[1] - answer[0]:
                answer = [l+1,r+1]
            gems_cnt[gems[l]] -= 1
            if gems_cnt[gems[l]] == 0:
                del gems_cnt[gems[l]] # 0개 되면 삭제
            l += 1
            
    return answer
```



