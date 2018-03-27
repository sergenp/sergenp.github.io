---
published: true
layout: post
title: Hackerrank - Mini-Max Problem
categories: Python
---
## Hackerrank Mini-Max problemi

Bu yazımda hackerrank daki algoritmalardan Mini-Max'ın çözümünü paylaşacağım. Büyük ihtimalle yaptığım bütün Hackerrank algorithm challengesleri bir seri halinde paylaşacağım. Ben problemleri python ile çözeceğim, istediğiniz programlama diline çevirebilirsiniz.

### Problemimiz

Bizden 5 uzunluğunda bir listenin, listeden bir rakam çıkartıp listeyi topladığımızda toplamının en düşük ve en yüksek değerini istiyor. Yani:
Girdi olarak verilen:
> 1 2 3 4 5

Çıktı olarak istenen:
> 10 14

Daha da açıklamak gerekirse:

-1 2 3 4 5, listesinden 1'i çıkarır gerisini toplarsak -> 2 + 3 + 4 + 5 = 14
-1 2 3 4 5, listesinden 2'yi çıkarır gerisini toplarsak -> 1 + 3 + 4 + 5 = 13
...
-1 2 3 4 5, listesinden 5'i çıkarır gerisini toplarsak -> 1 + 2 + 3 + 4 = 10

### Çözümüm

Eğer bizden listenin en düşük ve en yüksek toplamını istiyorsa,listenin öncelikle bütün elemanlarının toplamını alıp listedeki en büyük elementten çıkarırsak, minimum değerini, bütün elemanların toplamından en küçük elemanı çıkarırsak, maximum değerini buluruz
Python koduna gelirsek:
{% highlight python %}
#!/bin/python3

import os
import sys

#
# Complete the miniMaxSum function below.
#
def miniMaxSum(arr):
    min_in_arr = min(arr)
    max_in_arr = max(arr) 
    sum_all = 0
    for i in arr:
        sum_all += i
    max_sum = sum_all - min_in_arr
    min_sum = sum_all - max_in_arr
    print(min_sum, max_sum)
if __name__ == '__main__':
    arr = list(map(int, input().rstrip().split()))
    miniMaxSum(arr)
{% endhighlight %}


