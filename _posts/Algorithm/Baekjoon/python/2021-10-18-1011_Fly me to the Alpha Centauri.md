---
title: "[python] 1011 Fly me to the Alpha Centauri"
categories: [Algorithm, Baekjoon]
tags: [python]
---
```py3
import math 

T = int(input())

for _ in range(T):
  x, y = map(int, input().split())

  distance = y - x
  max = int(math.sqrt(distance))

  if distance == max ** 2: 
    print( 2 * max - 1 )
  elif max ** 2 < distance <= (max**2) + max:
    print( 2 * max )
  else:
    print( (2 * max) + 1 )```