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
last_modified_at: 2024-01-26
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

<br/>



#### 투 포인터 예제2(백준 온라인 저지 1940번)

1. 재료의 개수 n이 주어지고 이를 각 재료마다의 고유 번호가 존재한다.
2. 임의의 두개의 재료의 고유 번호 합을 구해서 주어진 m이 나온다면 두 쌍은 문제의 조건을 만족한다.
3. 이 때 이 두개의 쌍이 나올 수 있을만큼 카운트 하는 것이다.
4.  재료의 수가 최대 15000인데 $15000^2 > 2억$ 이므로 시간 복잡도 $O(n^2)$를 가지는 알고리즘을 사용하게 될 경우 제한 시간을 만족하지 못하게 된다.

  

수도 코드)

cin >> n;

cin >> m

vector< int > a(n, 0);

for(n만큼) {원소 채워주고}

int start_index = 0; 

int end_index = 1;

while(end_index = )

