---
layout: posts
title:  "[LeetCode] Word Search"
categories: ['Algorithm', 'LeetCode']



---

[문제링크](https://leetcode.com/problems/word-search/)

<br/>

###### 문제 설명

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

 

**Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.



<br/>



### 주절주절

옛날에 삼성 SW역량테스트를 준비했을때 많이 접했던 유형으로, 시뮬레이션을 진행하거나 말판의 말을 움직이는 문제여서 반가웠습니다. 

19년도 취준생 시절, 삼성 SW역량테스트 A형을 취득했던 경험이 있는데요. 이후론 A+형도 생겼다고 들었던 것 같습니다. 저 같은 경우 첫 직장의 최종 선택지는 카카오와 삼성전자, SK브로드밴드 였고 카카오를 선택했었습니다. 세 회사 모두 준비과정에서 집중했던 부분이 많이 달랐던 것으로 기억하는데요. 조만간 제가 개발직 취업 준비를 하며 회사별 집중했던 포인트를 한번 정리해 볼까 합니다.

정리해 볼 회사들은 현 직장과 전 직장인 SKT와 카카오, 최종합격을 경험한 삼성전자, 네이버, SK브로드밴드 정도로 예상 하고 있습니다. 

<br/>     

### Sol

풀이의 핵심은 현재위치를 기준으로 다음 word[idx] 가 사방에 존재하는지를 확인하는 bfs 입니다.

먼저, word[0] 이 board에 존재하지 않는다거나, word의 길이가 1이라거나, word안의 character들이 혹시 board에 존재하지 않는 것이 있는 경우와 같은 edge 케이스들을 사전에 처리해 준 후, 탐색을 시행했습니다.
candi라는 리스트를 통해 character가 하나씩 들어가면서 가능한 [행좌표, 열좌표, 직전에서 어떻게 이동해 왔는지] 의 정보들을 저장하게 했습니다.

또한 이미 방문한 곳은 재방문하지 않으며, 직전에서 현재위치로 어떻게 이동해 왔는지를 같이 기록하여 실행속도를 더 빠르게 하고자 했습니다. 



아래 코드를 통해 직관적으로 확인 가능합니다.



### Code

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m,n = len(board), len(board[0])
        candi, idx = [], 1
        dir_dic = {
            0: [[1,0], [-1,0],[0,-1], [0,1]], # 초기
            1: [[1,0], [0,-1], [0,1]],  # 상
            2: [[-1,0], [0,-1], [0,1]], # 하
            3: [[1,0], [-1,0], [0,1]],  # 좌
            4: [[1,0], [-1,0], [0,-1]]  # 우
        }
        dir_dic_nxt = {'[1, 0]': 1, '[-1, 0]': 2, '[0, 1]': 3, '[0, -1]': 4}

        for i in range(m):
            for j in range(n):
                if board[i][j] == word[0]:
                    candi.append([[i,j,0]])
        # 시작이 없을 경우 제외
        if len(candi) == 0:
            return False
        # word가 1개일 경우
        if len(word) == 1:
            return True
        
        # 존재하지 않는지 확인
        for _ in range(len(word)):
            exist = False
            for i in range(m):
                if word[_] in board[i]:
                    exist = True
                    break
            if not exist:
                return False
        
        while idx < len(word):
            nxt_candi = []
            for cand in candi:
                pos_i, pos_j = cand[-1][0], cand[-1][1]
                checklist = dir_dic[cand[-1][-1]] # 확인해야 할 위치 리스트
                for check in checklist:
                    nxt_i, nxt_j = pos_i + check[0],  pos_j + check[1]
                    # 다음 char 발견
                    if (-1 < nxt_i < m) and (-1 < nxt_j <n) and board[nxt_i][nxt_j] == word[idx] and [nxt_i, nxt_j] not in [_[:2] for _ in cand]:
                        nxt_candi.append(cand + [[nxt_i, nxt_j, dir_dic_nxt[str(check)]]])

            if len(nxt_candi) == 0:
                return False
            candi = nxt_candi
            idx += 1

        return True
```





