---
published: false
layout: post
categories: Python
tags:
  - algoritma
---
## Hackerrank - 2D Array - DS

Problemde bize 6x6 bir dizi veriliyor şöyle ki:

1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 2 4 4 0
0 0 0 2 0 0
0 0 1 2 4 0

Bizden verilen dizide "kum saatleri" bulup, bu kum saatlerinin hangisinin içindeki rakamların toplamı en büyük, onu çıktı olarak vermemizi söylüyor. Kum saatleride bu verilen 6x6 lık dizi için budur:

1 1 1   1 1 0   1 0 0   0 0 0
  1       0       0       0
1 1 1   1 1 0   1 0 0   0 0 0

0 1 0   1 0 0   0 0 0   0 0 0
  1       1       0       0
0 0 2   0 2 4   2 4 4   4 4 0

1 1 1   1 1 0   1 0 0   0 0 0
  0       2       4       4
0 0 0   0 0 2   0 2 0   2 0 0

0 0 2   0 2 4   2 4 4   4 4 0
  0       0       2       0
0 0 1   0 1 2   1 2 4   2 4 0

Ki bu verilen dizi için en yüksek toplama sahip kum saati:

2 4 4
  2
1 2 4

Yani çıktı olarak: 2 + 4 + 4 + 2 + 1 + 2 + 4 = 19 olmalı.

