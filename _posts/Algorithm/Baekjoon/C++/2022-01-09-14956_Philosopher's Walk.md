---
title: "[C++] 14956 Philosopher's Walk"
categories: [Algorithm, Baekjoon]
tags: [C++]
---

```C++
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'

pair<int, int> walk(int n, int m) {
  if (n == 2) {
    switch(m) {
      case 1: return {1, 1};
      case 2: return {1, 2}; 
      case 3: return {2, 2};
      case 4: return {2, 1}; 
    }
  }

  int r = (n * n) / 4; 
  if (m <= r) {
    pair<int, int> ch = walk(n/2, m);
    return {ch.second, ch.first}; 
  }
  else if (m <= r*2) {
    pair<int, int> ch = walk(n/2, m - r);
    return {ch.first, ch.second + n/2};
  }
  else if (m <= r*3) {
    pair<int, int> ch = walk(n/2, m - r*2);
    return {ch.first + n/2, ch.second + n/2}; 
  }
  else {
    pair<int, int> ch = walk(n/2, m - r*3);
    return {n - ch.second + 1, n/2 - ch.first + 1}; 
  }
}

int main(void) {
  ios_base::sync_with_stdio(false); cin.tie(NULL);
  
  int n, m, k; cin >> n >> m;

  pair<int, int> ans = walk(n, m);
  cout << ans.first << ' ' << ans.second;
} 

// 3,4 분면일떄는 뒤집고, 1,2 분면일때는 그대로 ```