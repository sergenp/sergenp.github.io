---
published: false
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

### Çözüm yolları


#### Benim ilk düşündüğüm çözüm yolu

Eğer bizden listenin en düşük ve en yüksek toplamını istiyorsa, o zaman listenin ilk olarak en düşük toplamını bulmak için, listenin en yüksek sayısını 0 a eşitler, gerisini birbiriyle toplarsak, toplamın en düşük değerini elde ederiz yani:
Liste
> 1 2 3 4 5

olursa, ve biz 5i(en yüksek değeri) 0 a eşitlersek,

Liste
> 1 2 3 4 0

olur. Ve hepsini toplarsak -> **1 + 2 + 3 + 4 + 0 = 10**, listemizin en düşük toplamı olur.
Aynı şekilde eğer biz 1i 0 a eşitleyip diğerlerini toplarsak -> **0 + 2 + 3 + 4 + 5 = 14** 
olur. Bu şekilde en düşük ve en yüksek toplamı bulmuş oluruz.

Python koduna gelirsek:
{% highlight python %}
#!/bin/python3

import os
import sys

#
# Complete the miniMaxSum function below.
#
def miniMaxSum(arr):
    org_arr = arr[:]
    min_in_arr = min(arr)
    max_in_arr = max(arr)
    if min_in_arr != max_in_arr:    
        max_sum = 0
        min_sum = 0
        for i,j in enumerate(arr):
            if j == min_in_arr:
                #print("does work")
                arr[i] = 0
                #print(arr[i])
            #print(j)
            max_sum += arr[i]
            #print(min_sum)
        arr = org_arr[:] 
        for i,j in enumerate(arr):
            if j == max_in_arr:
                arr[i] = 0
            min_sum += arr[i]
    else:
        min_sum = min_in_arr * (len(arr)-1) 
        max_sum = max_in_arr * (len(arr)-1)
    print(min_sum, max_sum)
            
if __name__ == '__main__':
    arr = list(map(int, input().rstrip().split()))
    miniMaxSum(arr)

{% endhighlight %}

Çözüm yöntemim pek "pythonic" değil, sanki daha da kısaltılabilirmiş gibi ki benim çözüm yöntemim dışındaki çözümler gayet kısaltılmış vaziyette. Açıklanması gereken bir iki satır olduğunu düşünüyorum.
{% highlight python %}
org_arr = arr[:] # bu nedir?
{% endhighlight %}

Biz listemizdeki en yüksek sayıyı yani 5 i 0 a eşitlediğimizde tahmin edebileceğiniz üzere o listemizi değiştirmiş oluyoruz. Bu listemizi tekrar eski haline getirmemiz gerek. O yüzden listemizi başka bir değişkene atıyoruz. Peki **":"** işareti ne işe yarıyor? Şöyle örnek verebiliriz:

{% highlight python %}
a = [1,2,3,4,5]
b = a
print(a)
>>> [1,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
a[0] = 0
print(a)
>>> [0,2,3,4,5]
print(b)
>>> [0,2,3,4,5]
{% endhighlight %}

Gördüğünüz gibi eğer a yı değiştirirsek, orjinal olmasını istediğimiz listemizdeki element de değişiyor, fakat biz şunlardan birini kullanırsak:
{% highlight python %}
a = [1,2,3,4,5]
b = list(a) # list() fonksiyonu
print(a)
>>> [1,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
a[0] = 0
print(a)
>>> [0,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
{% endhighlight %}

Veya:

{% highlight python %}
a = [1,2,3,4,5]
b = a[:] # [:]
print(a)
>>> [1,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
a[0] = 0
print(a)
>>> [0,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
{% endhighlight %}

Veya:

{% highlight python %}
import copy
a = [1,2,3,4,5]
b = copy.copy(a) # copy() fonksiyonu 
print(a)
>>> [1,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
a[0] = 0
print(a)
>>> [0,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
{% endhighlight %}

Veya:

{% highlight python %}
import copy
a = [1,2,3,4,5]
b = copy.deepcopy(a) # deepcopy() fonksiyonu 
print(a)
>>> [1,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
a[0] = 0
print(a)
>>> [0,2,3,4,5]
print(b)
>>> [1,2,3,4,5]
{% endhighlight %}

En sonuncu kopyalama yöntemi gerçekten yavaş.














