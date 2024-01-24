---
layout: single
title:  "알고리즘 - 배열, 리스트, 벡터 - 투 포인터"
excerpt: "Do it! 알고리즘 코딩 테스트 - C++편"

categories: Algorithm
tag: [Cpp, Algorithm, Two Pointer]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-01-24
last_modified_at: 2024-01-24
---

## 투 포인터

<br/>

### 문제



#### 연속된 자연수의 합 구하기(백준 온라인 저지 2018번)

1. 자연수가 주어졌을 때, 그 자연수를 연속된 자연수의 합으로 나타내는 경우의 수
2. 입력되는 수의 최댓값이 매우 크므로 $O(n)$의 시간복잡도를 사용하여야 힌다.
3.  투 포인터를 이용한다. 즉, start_index, end_index를 사용한다.

수도코드)

start_index, end_index = 1;

while(end_index != n){

​	sum == n인 경우 end_index++; sum += end_index; count++;

​	sum <n 인경우 end_index++; sum+= end_index;

​	sum >n 인경우 start_index--; sum-=start_index;

}



```cpp
  #include <iostream>
  #include <vector>
  using namespace std;

  int main(){
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    int n;
    cin >> n;

    int sum = 1;
    int start = 1;
    int end = 1;
    int cnt = 1;
    while(end != n){
      if(sum == n){
        cnt ++;
        end++;
        sum += end;
      }
      else if(sum < n){
        end++;
        sum += end;
      }

      else if(sum > n){
        sum-=start;
        start++;
      }
    }
    cout << cnt << '\n';


  }

```

