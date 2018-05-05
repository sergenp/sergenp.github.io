---
published: true
layout: post
categories: Python
tags:
  - algoritma
title: Hackerrank - 2D Array - DS
---
## Hackerrank - 2D Array - DS

### Problem
Problemde bize 6x6 bir dizi veriliyor şöyle ki:
<pre>
1  1  1  0  0  0    
0  1  0  0  0  0  
1  1  1  0  0  0  
0  0  2  4  4  0  
0  0  0  2  0  0  
0  0  1  2  4  0
</pre>

Bizden verilen dizide "kum saatleri" bulup, bu kum saatlerinin hangisinin içindeki rakamların toplamı en büyük, onu çıktı olarak vermemizi söylüyor. Kum saatleride bu verilen 6x6 lık dizi için budur:
<pre>
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
</pre>
Ki bu verilen dizi için en yüksek toplama sahip kum saati:

<pre>
2 4 4
  2
1 2 4
</pre>

Yani çıktı olarak: 2 + 4 + 4 + 2 + 1 + 2 + 4 = 19 olmalı.

### Çözüm

#### Düşüncem

Bizim listemiz, 
{% highlight python %}
liste = [[1, 1, 1, 0, 0, 0], [0, 1, 0, 0, 0, 0], [1, 1, 1, 0, 0, 0], [0, 9, 2, -4, -4, 0], [0, 0, 0, -2, 0, 0], [0, 0, -1, -2, -4, 0]]
{% endhighlight %}

liste[0][0] bize 1. elemanın 1.elementini verdiğini biliyoruz. liste[0][1], 1.satırın 2.elementi, liste[0][2], 1.satırın 3.elementi.... Yani elimizde bir matris var.

Listemizin 1.satırı başlangıç olarak ele aldığımızda(liste[0]), ilk kum saatimiz:
<pre>
liste[0][0]  liste[0][1]  liste[0][2]
             liste[1][1]  
liste[2][0]  liste[2][1]  liste[2][2]  
</pre>

##### Eee?

Bize verilen soruda girilecek matrisin her zaman 6x6 olduğu söyleniyor. Bu yüzden kum saati sayımız sabit, yani 16 tane.  
Bu mantıkla yola çıkarsak, listemizin üstünden satır ve sütun olarak geçmek ve 16 tane kum saati bulmamız lazım.  
i = satır pozisyonu  
j = sütun pozisyonu  

olsun. İlk kum saatimiz için genelleştirme yaparsak,  
**i = 0 için, j = 0, 1, 2 ---> ilk satır  
i = 1 için, j =    1	---> ikinci satır  
i = 2 için, j = 0, 1, 2 ---> üçüncü satır**  
olmalı ki bize ilk kum saatimiz verilsin. Peki 2. kum saati?:  
**i = 0 için, j = 1, 2, 3  
i = 1 için, j =    2  
i = 2 için, j = 1, 2, 3**
olmalı.

_**j == 3**_ olduğu zaman listenin sonuna gelmiş oluyoruz. Yani _**i**_ yi 1 arttırmamız lazım.  
  
**i = 0 için, j = 3, 4, 5  
i = 1 için, j =    4  
i = 2 için, j = 3, 4, 5**
1.satır için son kum saatini verir. Ve 2.satıra geçeriz:  
**i = 1 için, j = 0, 1, 2 
i = 2 için, j =    1  
i = 3 için, j = 0, 1, 2**



##### Kod olarak yazarsak.

{% highlight python %}
def array2D(liste):
	# Verilen listede her liste[i][j] için -9<=liste[i][j]<=9 olduğu söyleniyor. Yani bir kum saati toplamının alabileceği minumum değer -9 * 7 = -63 olur. Bu yüzden sum_val değerimiz -64 den başlamalı.
    sum_val = -64
    # Verilen 6x6 listede 16 kum saati olduğu kesin
    for i in range(4):
        for j in range(4):
            temp = sum(liste[i][j:j+3]) + liste[i+1][j+1] + sum(liste[i+2][j:j+3])
            if sum_val < temp:
                sum_val = temp
    return sum_val
{% endhighlight %}

Burada açıklamak gerekilen tek yer herhalde, **liste[i][j:j+3]** özellikle "**[j:j+3]**" kısmı olabilir.Python da listelerden bir dilim almak için yaptığımız bir syntax.Örnek verilecek olursa:

{%highlight python%}
>>> a = [0,1,2,3,4,5]
>>> a[2:5]
[2, 3, 4]
>>> a[1:3]
[1, 2]
>>> a[0:5]
[0, 1, 2, 3, 4]
>>> a[4:6]
[4, 5]
>>> a[1:-2] # a[:-2] demek listenin son 2 elemanını kes, gerisini dönder demek. Yani a[:-2] = a[0:len(a) - 2]
[1, 2, 3]
{% endhighlight %}

Görüldüğü üzere bir dilim almak için, liste[başlangıç_indexi:bitiş_indexi] dememiz yeterli.Eğer:  
liste = [0,1,2,3,4,5]  
başlangıç_indexi = 2  
bitiş_indexi = 5  
Olursa,  
liste[başlangıç_indexi:bitiş_indexi] = liste[2:5] -----> [liste[2], liste[3], liste[4]]  
olarak bir liste geri dönderir. 
> Verilen başlangıç_indexindeki değer listeye dahilken, bitiş_indexinin değeri listeye dahil değildir.

Ve bu sum() fonksiyonu ne derseniz, Pythonun kendi build-in fonksiyonlarından biri. Bir **iterable**(list, dict, tuple...) alıp bu iterable nin elementlerinin toplamını dönderir. Daha fazla bilgi için [sum()](https://www.programiz.com/python-programming/methods/built-in/sum)
