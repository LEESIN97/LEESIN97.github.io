---
layout: single
title:  "[알고리즘 C++] 배열, 리스트, 벡터"
excerpt: "Do it! 알고리즘 코딩 테스트 - C++편"

categories: AlgorithmCpp
tag: [Algoritm_C++]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-01-17
last_modified_at: 2024-01-23
---

## 배열, 리스트, 벡터

<br/>



<br/>





### 배열

- 인덱스를 사용하여 값에 바로 접근할 수 있다.
- 새로운 값을 삽입하거나 특정 인덱스에 있는 값을 삭제하기 어렵다.
- 배열의 크기는 선언할 때 지정할 수 있으며, 한번 선언하면 크기를 변경할 수 없다.



<br/>

<br/>



### 리스트

- 노드를 포인터로 연결한 자료구조
- 인덱스가 없으므로 Head포인트부터 순서대로 접근해야한다. 즉, 속도가 느리다.
- 포인터로 연결되어 있으므로 데이터를 삽입하거나 삭제하는 연산 속도가 빠르다.
- 선언할 때 크기를 별도로 지정하지 않는다. 즉, 리스트는 변하기 쉬운 데이터를 다룰 때 적절하다.
- 포인터를 저장할 공간이 필요하므로 배열보다 구조가 복잡하다.

<br/>



<br/>



### 벡터

- 동적으로 원소를 추가할 수 있다. 즉, 크기가 자동으로 늘어난다.
- 맨 마지막 위치에 데이터를 삽입하거나 삭제할 때는 문제가 없지만 중간 데이터의 삽입 삭제는 배열과 같은 메커니즘으로 동작한다.
- 배열과 마찬가지로 인덱스를 이용하여 각 데이터에 접근할 수 있다.

<br/>



<br/>





### 문제

<br/>

##### 숫자의 합 구하기 (백준 온라인 저지 11720)

숫자의 개수, 공백없이 주어진 N개의 숫자가 순서대로 입력이 된다.

이때 자료구조는 벡터 또는 배열로 사용한다. N개의 자릿수를 가진 숫자의 순서는 중요하지 않고 단순히 더하는 것이기 때문에 리스트를 사용하지 않고 벡터 또는 배열로 사용한다.

각 자리의 숫자를 각각 더해야 하므로 이룰 나눠서 나머지를 구하는 방법도 있겠지만, 입력 받은 숫자를 바탕으로 char배열을 만들어 각 자리의 문자를 int형으로 바꿔 더해준다. 

<br/>



수도 코드)

cin >> n;

char s[n+1];

cin >> s;

int ans = 0;

for(문자열 길이만큼 인덱싱) { 각 인덱스에서의 문자를 정수로 바꿔서 ans에 더한다.}

cout << ans;

<br/>



이때 문자를 숫자로 변환하기 위해서는 다음과 같은 방법들을 이용한다.

```c++
int n = '1' - 48 // 숫자 '1'은 아스키코드 값이 49이므로 n은 1의 정수 값을 가지게 된다.
```

```c++
#include <string>
string sNUM = "1234";
string sNum_d = "1234.56";
int inum = stoi(sNum);
long lnum = stol(sNum);
double dnum = stod(sNum_d);
float fnum = stof(sNum_d);
```

숫자를 문자로 변환하기 위해서는 다음과 같은 방법을 이용한다.

```cpp
#include <string>

int inum = 1234;
int lnum = 1234;
double dnum = 1234.56;
float fnum = 1234.56f;
string intToString = to_string(inum);
string longToString = to_string(lnum);
string doubleToString = to_string(dnum);
string floatToString = to_string(fnum);

```



<br/>

<br/>

##### 평균 구하기 (백준 온라인 저지 1546번)

1. 먼저, 입력받은 순서는 중요하지않고 입력 개수가 주어지기 때문에 배열 혹은 벡터를 사용하면 된다.

2. 최대값을 먼저 구한다. 
3. 최대값을 구했다면 구해진 최대값으로 원래 값들을 수정한다.
4. 최종 평균값을 계산한다.

수도 코드)

cin >> n;

int score[n];

int max = 0;

for(score의 길이만큼){ max 보다 크다면 max 갱신}

for(score의 길이만큼){ score[i]값 갱신}

cout << socre의 총합 / score의 길이 

```cpp
  #include <iostream>

  using namespace std;

  int main(){
    int n;
    cin >> n;
    float score[n];
    int max = 0;

    // get max
    for(int i=0; i<n; i++){
      cin >> score[i];
      if(max < score[i]) max = score[i];
    }

    for(int i=0; i<n; i++){
      score[i] = score[i] / (float)max * 100;
    }

    float sum = 0;
    for(int i=0; i<n; i++)
    {
      sum += score[i];
    }
    float average = 0;
    average = sum / (float)n;
    cout << average << endl;

  }

```

