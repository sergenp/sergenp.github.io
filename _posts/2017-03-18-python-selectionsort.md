---
published: true
layout: post
title: 'Python ile Algoritmalar:Selection Sort '
categories: Python
tags: 
- algoritma
---
Selection short, bubble shortun biraz daha gelişmiş hali diyebiliriz, listenin üzerinden her geçişinde sadece 1 swap yapıyor. Şöyle gösterilebilir:


![]({{site.baseurl}}/images/selectionsort/selectionsortnew.png)


veya:


![]({{site.baseurl}}/images/selectionsort/Selection-sort-algorithm.jpg)


Pythonla bunu nasıl yapabiliriz peki?



{% highlight python %}

def selectionSort(alist):
   for doldur in range(len(alist)-1,0,-1):
       maxSayiPozisyonu=0
       for yer in range(1,doldur+1):
           if alist[yer]>alist[maxSayiPozisyonu]:
               maxSayiPozisyonu = yer

       temp = alist[doldur]
       alist[doldur] = alist[maxSayiPozisyonu]
       alist[maxSayiPozisyonu] = temp

alist = [54,26,93,17,77,31,44,55,20]
selectionSort(alist)
print(alist)

{% endhighlight %}

{% highlight python %}
   for doldur in range(len(alist)-1,0,-1):
{% endhighlight %}

Gördüğünüz gibi liste uzunluğu kadar işlem yapacağız.Direk algoritma hızı için (n-1) çarpanımız burdan gelmekte.

{% highlight python %}
   for doldur in range(len(alist)-1,0,-1):
       maxSayiPozisyonu=0
       for yer in range(1,doldur+1):
           if alist[yer]>alist[maxSayiPozisyonu]:
               maxSayiPozisyonu = yer
{% endhighlight %}
Bu döngümüzü çalıştıralım,
alist = [20,62,23,12] olsun kolaylık açısından
{% highlight python %}
doldur == 3 # için:
	maxSayiPozisyonu = 0
    for yer in range(1,4): 
    	#yer = 1 için
    	if alist[1] > alist[0]: # ilk geçişimizde alist[1] = 62 ve alist[0] = 20 olur ve 62>20 için 
        	maxSayiPozisyonu = 1 # maxSayiPozisyonu=1 değerini alır
     	#yer = 2 için
        if alist[2] > alist[1] # ki bu ifade 23 > 62 olmayacağından doğru değildir.
        	maxSayiPozisyonu = 2 # maxSayiPozisyonu=2 değerini almaz.
        #yer = 3 için
        if alist[3] > alist[1] # ki bu ifade 12 > 62 olmayacağından doğru değildir.
        	maxSayiPozisyonu = 3 # maxSayiPozisyonu=3 değerini almaz.

	#yer değiştirilir:
       temp = alist[3]
       alist[3] = alist[1]
       alist[1] = temp
       
    #doldur == 3 için döngünün sonunda alist değerimiz:
    #>>> [20,12,23,62]
{% endhighlight %}
Böylelikle ilk döngünün sonunda, en büyük sayımız listenin en sonuna konulmuş oldu.

{% highlight python %}
alist = [20,12,23,62] # olmuştu
doldur == 2 # için:
	maxSayiPozisyonu = 0
    for yer in range(1,3): 
    	#yer = 1 için
    	if alist[1] > alist[0]: # ilk geçişimizde alist[1] = 12 ve alist[0] = 20 olur ve 12>20 için 
        	maxSayiPozisyonu = 1 # maxSayiPozisyonu=1 değerini almaz
     	#yer = 2 için
        if alist[2] > alist[1] # ki bu ifade 23 > 12 olacağından doğrudur.
        	maxSayiPozisyonu = 2 # maxSayiPozisyonu=2 değerini alır.

	#ve alışık olduğumuz yer değiştirme işlemi gerçekleşir:
       temp = alist[2] 	#temp = alist[doldur]
       alist[2] = alist[2]	#alist[doldur] = alist[maxSayiPozisyonu]
       alist[2] = temp	#alist[maxSayiPozisyonu] = temp
       
    #doldur == 2 için döngünün sonunda alist değerimiz:
    #>>> [20,12,23,62] olur, yani değişmez
{% endhighlight %}
Ve en son olarakta:

{% highlight python %}
alist = [20,12,23,62] # olmuştu
doldur == 1 # için:
	maxSayiPozisyonu = 0
    for yer in range(1,2): 
    	#yer = 1 için
    	if alist[1] > alist[0]: # ilk geçişimizde alist[1] = 12 ve alist[0] = 20 olur ve 12>20 yanlış olduğu için 
        	maxSayiPozisyonu = 1 # maxSayiPozisyonu=0 değerinde kalır
            
	#yer değiştirme işlemi gerçekleşir:
       temp = alist[1] 	#temp = alist[doldur]
       alist[1] = alist[0]	#alist[doldur] = alist[maxSayiPozisyonu]
       alist[0] = temp	#alist[maxSayiPozisyonu] = temp
       
    #doldur == 1 için döngünün sonunda alist değerimiz:
    #>>> [12,20,23,62] olur
{% endhighlight %}

Ve en sonundada listemiz sıralı bir vaziyet almış olur.

## Algoritmanın Hızı

Algoritma bubble sort ile aynı hıza sahip,yani, (n-1.n-2 / 2) == O(n^2).Ama benchmarklarda daha az yer değiştirme yaptığı için daha iyi sonuçlar elde ediyor.Bubble sortun biraz daha geliştirilmiş versiyonu denilebilir.
