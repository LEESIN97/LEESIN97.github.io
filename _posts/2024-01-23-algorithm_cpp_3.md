---
layout: single
title:  "알고리즘 - 배열, 리스트, 벡터 - 구간 합"
excerpt: "Do it! 알고리즘 코딩 테스트 - C++편"

categories: AlgorithmCpp
tag: [Cpp, algorithm, Part Sum]

toc: true
toc_sticky: true

author_profile: true
sidebar: true

search: true

date: 2024-01-23
last_modified_at: 2024-01-24
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

<br/>

### 구간 합 구하기 2 (백준 온라인 저지 11660번)

1. 앞 문제의 2차원 버전이다.

2. 마찬가지로 합 배열을 먼저 구한다.

3. 2차원 table로 구간 합 배열을 구한다. -> 문제에서 요구하는 것이 두 인덱스 좌표를 주면, 그 두개의 좌표로 이루어지는 사각형에서의 모든 값의 총합을 구하는 것이다. 이를 최대한 시간복잡도를 줄이기 위해 합 배열을 구할 때 다음과 같은 로직을 따른다.

   ```cpp
   s[i][j] = s[i][j-1] + s[i-1][j] - s[i-1][j-1] + a[i][j]; // 중복되는 값은 빼주고 새로운 값은 더해줌
   ```

   그리고 결과값은 다음과 같이 구한다.

   ```cpp
   s[x2][y2] - s[x1-1][y2] - s[x2][y1-1] + s[x1-1][y1-1]; // 두번 빼준 값은 다시 더해줌
   ```

   

4. 각 테스트 케이스 마다의 구간 합을 출력한다.

수도 코드)

cin >> n >> m;

int a[ n+1 ] [ n+1] = {};

int s[ n+1 ] [ n+1] = {};

for( 1~ n)

​	for(1~n) {원본 테이블 생성}

for( 1~ n)

​	for(1~n) {합 배열 저장  }

for( test case m만큼) { cin >> x1 >> y1 >> x2 >> y2 ; 결과값 출력}



```cpp
#include <iostream>

using namespace std;

int main(){
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);

  int n, m;
  cin >> n >> m;


  int a[n+1][n+1];
  int s[n+1][n+1];
  for(int i=1; i<=n; i++){
    for(int j=1; j<=n; j++){
      cin >> a[i][j];
      s[i][j] = s[i][j-1] + s[i-1][j] - s[i-1][j-1] + a[i][j];
    }
  }
  for(int i=0; i<m; i++){
    int x1, y1, x2, y2;
    cin >> x1 >> y1 >> x2 >> y2;
    int ans = s[x2][y2] - s[x1-1][y2] - s[x2][y1-1] + s[x1-1][y1-1];
    cout << ans << '\n';
  }




}

```

결과값을 출력할 때 cout << endl 을 사용해서 시간초과가 났는데 cout << '\n' 을 하는 경우에는 됐었음.

'\n'을 쓰는 것이 개행 문자만을 출력하므로 시간 초과가 나지 않았던 것이므로 앞으로 이를 사용.







<br/>

### 나머지 합 구하기(백준 온라인 저지 10986번)

1. N개의 수가 주어졌을 때 연속된 부분의 합이 M으로 나누어 떨어지는 구간의 개수를 구하는 문제
2. 마찬가지로 입력 받은 수를 바탕으로 합 배열을 만든다.
3. 합 배열의 차를 이용하여 두 쌍의 인덱스 구간의 합을 구할 수 있다.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);

  int n, m;
  cin >> n >> m;
  vector<long> s(n, 0);
  int tmp;
  for(int i=1; i<=n; i++){
    cin >> tmp;
    s[i] = s[i-1] + tmp;
  }

  int cnt = 0;

  for(int i=1; i<=n; i++){
    for(int j=0; j<i; j++){
        int tmp = s[i] - s[j];
        if(tmp % m == 0) cnt++;

    }
  }
  cout << cnt << '\n';


}

```

이 코드로는 제한 시간 1초를 맞출 수 없었다.



**나머지 합 문제 풀이의 핵심 아이디어**

: 특정 구간 수들의 나머지 연산을 더해 나머지 연산을 한 값과 이 구간 합의 나머지 연산을 한 값은 동일.

1. 합 배열의 요소 각각을 m으로 나눈 배열을 하나 생성한다.
2. 나머지가 0인 개수 만큼 카운트 해준다.
3. 나머지가 같은 두쌍의 조합의 개수만큼 카운트 해준다.

```cpp
 #include <iostream>
#include <vector>
using namespace std;

int main(){
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);

  int n, m;
  cin >> n >> m;
  vector<long> s(n+1, 0);
  int tmp;
  for(int i=1; i<=n; i++){
    cin >> tmp;
    s[i] = s[i-1] + tmp;
  }
  vector<int> remain(m, 0);

  int cnt = 0;
  for(int i=1; i<=n; i++){
    int remainder = s[i] % m;
    if(remainder == 0) cnt++;
    remain[remainder]++;
  }


  for(int i=0; i<m; i++){
    if(remain[i] > 1){
      cnt += remain[i]*(remain[i] - 1) / 2;}
  }


  cout << cnt << '\n';


}

```

