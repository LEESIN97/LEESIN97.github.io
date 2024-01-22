---
layout: single
title:  "알고리즘 - 배열, 리스트, 벡터 - 구간 합"
excerpt: "Do it! 알고리즘 코딩 테스트 - C++편"

categories: Algorithm
tag: [Cpp, algorithm, 구간 합]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-01-23
last_modified_at: 2024-01-23
---

## 구간 합

<br/>

구간합은 합 배열을 이용하여 시간 복잡도를 줄이는 특수한 목적의 알고리즘이다.



**" 구간 합의 핵심 이론"**

**합 배열을 구하면 기존 배열의 일정 범위의 힙을 구하는 시간 복잡도 $O(n^2)에서 O(1)$로 감소한다.** (최악의 경우가 상수 시간으로)



- 합 배열 S를 만드는 공식

```cpp
S[i] = S[i-1] + A[i]; 
```

- 구간 합을 구하는 공식

```cpp
S[j] - S[i-1] // i에서 j까지 구간 합
```

<br/>

<br/>

## 문제

<br/>

### 구간 합 구하기 1 (백준 온라인 저지 11659번)

1. 수 N개가 주어졌을 때 i번째 수에서 j번째 수까지의 합을 구하는 프로그램
2. 먼저 합 배열 S를 만든다.
3. 그리고 주어진 index의 구간합을 구하기 위해 합 배열 S를 이용한다.

수도 코드)

int n; //수의 개수

int m; //합을 몇번 구할지

cin >> n;

int array[n];

for(n길이만큼) {array생성}

long s[n] ={0, } // 합 배열

long s[0] = array[0] // 초기값 설정

for(i=1; i<n; i++){s[i] = s[i-1] + A[[i];]}

for(m만큼){구간합 구해서 출력}

```cpp
#include <iostream>

using namespace std;

int main(){

  ios::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);

  int n, m;
  cin >> n >> m;
  int s[100001] = {};

  for(int i=1; i<=n; i++){
    int temp;
    cin >> temp;
    s[i] = s[i-1] + temp;
  }

  for(int i=0; i<m; i++){
    int start, end;
    cin >> start >> end;
    cout << s[end] - s[start-1] << "\n";
  }


}

```

시간 단축을 위해 다음을 꼭 써주자.

```cpp
ios::sync_with_stdio(false);
cin.tie(NULL);
cout.tie(NULL);
```

첫번째 줄은 C의 stdio와 C++의 iostream 동기화를 비활성화 하여 C++의 독립버퍼 사용으로 수행속도가 빨라지게 하는 효과가 발생한다.

두번째 세번째 줄은 기본적으로 cin과 cout이 하나로 묶였는데, 하나로 묶인 두 스트림을 푼다. 즉, 한 스트림이 다른 스트림에서 각 IO 작업을 진행하기 전 자동으로 버퍼를 비워주는 것을 보장한다. 





