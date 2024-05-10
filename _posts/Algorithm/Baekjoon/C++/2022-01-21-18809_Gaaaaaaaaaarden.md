---
title: "[C++] 18809 Gaaaaaaaaaarden"
categories: [Algorithm, Baekjoon]
tags: [C++]
---

```C++
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'

struct d { int X, Y; }; 
vector<d> q;

int n, m, G, R, qs, ans, cnt;
int board[52][52], arr[10];
int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, -1, 0, 1}; 

int Gaaaaaaaaaarden() {
  cnt = 0; 
  queue<d> fq; 
  pair<int, int> st[52][52]; 
  

  for (int i=0; i < qs; i++)
    if (arr[i] == 1 || arr[i] == 2) {
      fq.push({q[i].X, q[i].Y});
      st[q[i].X][q[i].Y] = {0, arr[i]};
    }
  
  while(!fq.empty()) {
    auto cur = fq.front(); fq.pop(); 
    int curtime = st[cur.X][cur.Y].first;
    int curcolor = st[cur.X][cur.Y].second;
    if (st[cur.X][cur.Y].second == 3) continue;
    for (int i=0; i < 4; i++) {
      int nx = cur.X + dx[i];
      int ny = cur.Y + dy[i]; 
      if (nx < 0 || ny < 0 || nx >= n || ny >= m) continue; 
      if (board[nx][ny] == 0) continue;
      
      if (st[nx][ny].second == 0) {
        st[nx][ny] = {curtime+1, curcolor};
        fq.push({nx, ny}); 
      }
      else if (st[nx][ny].second == 1) {
        if (curcolor == 2 && st[nx][ny].first == curtime+1) {
          cnt++;
          st[nx][ny].second = 3;  
        }
      }
      else if (st[nx][ny].second == 2) {
        if (curcolor == 1 && st[nx][ny].first == curtime+1) { 
          cnt++;
          st[nx][ny].second = 3; 
        }
      }
    }
  }

  return cnt;
}

int main(void) {
  ios::sync_with_stdio(false); cin.tie(NULL);

  cin >> n >> m >> G >> R; 
  for (int i=0; i < n; i++)
    for (int j=0; j < m; j++) {
      cin >> board[i][j]; 
      if (board[i][j] == 2) q.push_back({i, j}); 
    }

  qs = q.size();
  fill(arr+qs-G-R, arr+qs-R, 1);
  fill(arr+qs-R, arr+qs, 2); 
  do {
    ans = max(ans, Gaaaaaaaaaarden());
  } while (next_permutation(arr, arr+qs)); 

  cout << ans; 
}```