---
layout: posts
title:  "[LeetCode] Median of Two Sorted Arrays"
categories: ['Algorithm', 'LeetCode']

---

[문제링크](https://leetcode.com/problems/median-of-two-sorted-arrays/)

<br/>

- Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

  The overall run time complexity should be `O(log (m+n))`.

   

  **Example 1:**

  ```
  Input: nums1 = [1,3], nums2 = [2]
  Output: 2.00000
  Explanation: merged array = [1,2,3] and median is 2.
  ```

  **Example 2:**

  ```
  Input: nums1 = [1,2], nums2 = [3,4]
  Output: 2.50000
  Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
  ```

  **Example 3:**

  ```
  Input: nums1 = [0,0], nums2 = [0,0]
  Output: 0.00000
  ```

  **Example 4:**

  ```
  Input: nums1 = [], nums2 = [1]
  Output: 1.00000
  ```

  **Example 5:**

  ```
  Input: nums1 = [2], nums2 = []
  Output: 2.00000
  ```

   

  **Constraints:**

  - `nums1.length == m`
  - `nums2.length == n`
  - `0 <= m <= 1000`
  - `0 <= n <= 1000`
  - `1 <= m + n <= 2000`
  - `-106 <= nums1[i], nums2[i] <= 106`

<br/>

### Sol

리트코드 Top 100 Interview 문제 중 Hard 난이도 문제였습니다.

항상 느끼는 거지만, 리트코드의 문제들은 얼마나 더 빠르고 효율적으로 푸느냐에따라 큰 차이가 있고,

저처럼 설렁설렁 패스만 할 정도로 푸는것에는 그래도 관대하다는(?) 느낌을 받습니다.

<br/>

이 문제는 딱 보자마자 Heap을 사용해야겠구나 라는 생각이 들었습니다.

이분탐색 문제를 풀면서 한번 주절주절 언급드린 적이 있는데, 저는 코테준비를 한참 하던 시절에

항상 Time Limit에 발목을 잡히곤 했습니다. 

그리고 '이분탐색, 스택, 힙, DP'는 그 당시 코테만 보면 탈락의 고배를 마셨었던 저에게 

정말 유용한 무기가 되어주었습니다.

  <br/>

특히 이 문제처럼O(log (m+n)) 이라는 빡빡한 Time Complexity를 요구하는 문제는 꼭 '힙'을 떠올리시면 좋습니다.

파이썬의 경우 힙을 활용하기 너무나 좋은 heapq라는 라이브러리가 있으므로 더할나위 없겠죠.



<br/>

힙을 활용한 문제를 더 연습하고 싶은 분들에겐 프로그래머스 코딩테스트 고득점 Kit의 힙 문제들을 추천합니다!

(조만간 고득점 Kit 문제들도 모두 다루겠습니다.)

[프로그래머스-더 맵게](https://programmers.co.kr/learn/courses/30/lessons/42626)

[프로그래머스-디스크 컨트롤러](https://programmers.co.kr/learn/courses/30/lessons/42627)

[프로그래머스-이중우선순위큐](https://programmers.co.kr/learn/courses/30/lessons/42628)

또한, 최근에 제 블로그에서 다룬 LeetCode의 First Missing Positive 문제도 추천합니다.

[LeetCode - First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

- [First Missing Positive 풀이]:https://guard1000.github.io/algorithm/leetcode/LeetCode-First-Missing-Positive/

  



<br/>

![image](https://github.com/guard1000/guard1000.github.io/blob/master/imgs/%5BLeetCode%5D%20Median%20of%20Two%20Sorted%20Arrays_1.png?raw=true)

문제 풀이는 위 사진 한장으로 설명됩니다.

1. 먼저 입력된 nums1과 nums2를 합쳐 줍니다. 

2. len(nums)가 홀수/짝수 여부를 몫과 나머지를 구해주는 divmod로 구해줍니다.

3. 리스트 nums를 heapq의 heapify 함수로 최소힙으로 변환해 줍니다. 

4. nums에 짝수개의 원소가 있다면, 2개의 median 값들의 평균을 구해야 합니다.

    몫-1 번 heappop()을 통해 median으로 접근한 후

   2번의 heappop()으로 구해지는 두 값의 평균을 반환합니다.

   <br/>

   만약 nums에 홀수개 원소가 있다면, 

   몫 번 heappop()을 통해 median으로 접근한 후

   nums[0]이 median 입니다.

<br/>

위 그림의 오른쪽에는 이해를 돕기 위해 문제의 Example2가 각 단계별 어떻게 돌아가 답을 내는지를 확인할 수 있습니다.

로직이 단계별로 어떻게 동작하는지를 따라가며 이해해 봅시다.

<br/>

참고로, heapq 라이브러리의 사용한 함수별 Time Complexity는 다음과 같습니다.

- heapify()  -> O(N)
- heappop() -> O(logN)



<br/>

### Code

```python
import heapq
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        answer = 0
        nums = nums1 + nums2
        if len(nums) == 0:
            return 0
        
        quotient, remainder = divmod(len(nums),2)
        heapq.heapify(nums)
        
        if remainder == 0: # 짝수
            for _ in range(quotient-1):
                heapq.heappop(nums)
            for _ in range(2):
                answer += heapq.heappop(nums)
            return answer/2
        
        else:               # 홀수
            for _ in range(quotient):
                heapq.heappop(nums)
            answer = heapq.heappop(nums)
            return answer 
```
