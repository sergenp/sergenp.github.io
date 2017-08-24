---
published: true
layout: post
categories: Python
title: 'Python ile Algoritmalar:Bubblesort '
tags: 
- algoritma
---
Algoritmaları öğrenmek için en iyi dilin python olduğuna karar verdim, öğrenmesi çok kolay, syntax derdi yok, binlerce librarisi var, yapamayacağınız hiçbişey yok. Tabii sorunlarıda mevcut. Bu konulara girmeden algoritmamız olan The Bubble Sort u inceleyelim.

## Bubblesort

Algoritmayı anlatmak gerekirse, algoritma listedeki ilk sayımızı alıyor(ilk geçişinde) ikincisiyle karşılaştırıyor, eğer ilk sayı ikinciden büyükse, ilk sayı ile ikinci sayının yerini değiştiriyor ve ilk sayı ile üçüncü sayıyı karşılaştırıyor.Eğer değilse bu sefer ikinci sayıyı üçüncü ile karşılaştırıp aynı işlemleri uyguluyor.Görselde iyi bi şekilde anlattım:
![bubble-sort-pythonla.png]({{site.baseurl}}/images/bubblesort/bubble-sort-pythonla.png)

Hatta daha iyi bi şekilde anlatılmış bir görsel var:
![bubble-short.png]({{site.baseurl}}/images/bubblesort/bubble-short.png)

Bunu nasıl koda dökeceğiz, geldik asıl kısmına tabii. 

{% highlight python %}
def bubbleSort(alist):
    for gecisSayisi in range(len(alist)-1,0,-1):
        for i in range(gecisSayisi):
            if alist[i]>alist[i+1]:
                temp = alist[i]
                alist[i] = alist[i+1]
                alist[i+1] = temp

alist = [54,26,93,17,77,31,44,55,20]
bubbleSort(alist)
print(alist)
{% endhighlight %}

Bu kadar basit. Hemen loopa bakalım, nasıl çalışıyor.

{% highlight python %}
for gecisSayisi in range(len(alist)-1,0,-1)
{% endhighlight %}

Burası gecisSayisi variablemizin len(alist) yani listenin uzunluğu - 1 den başlayıp, 0 a kadar, -1 azalarak değerler almasını sağlıyor. Bizim verdiğimiz listenin uzunluk sayısı 9 - 1, geçiş sayısı 8 oluyor.

Çalıştırıp bakalım,
{% highlight python %}

for gecisSayisi in range(8,0,-1) # girdiğimiz listeye göre alınan değer,
	for i in range(8) # ilk çalıştırdığımızdaki değer
    	# i = 0 için;
        if alist[0] > alist[1] # burayı açıklamaya gerek yok sanırım
          temp = alist[0] # geçici variable temp = alist[1] e eşit
          alist[0] = alist[1] # alist[0] > alist[1] olduğu için, alist[0] ve alist[1] nin yerlerini değiştir.
          alist[1] = temp # alist[1] de temp e eşit, yani alist[0] la alist[1] in yeri değişmiş oldu 
          
#>>> temp = alist[0]
#>>> print(temp)
#54
#>>> alist[0] = alist[1]
#>>> print(alist)
#[26, 26, 93, 17, 77, 31, 44, 55, 20]
#>>> alist[1] = temp
#>>> print(alist)
#[26, 54, 93, 17, 77, 31, 44, 55, 20]
{% endhighlight %}

İlk geçişimizde kısaca bunu yapmış olduk, i = 1 için bakalım birde

{% highlight python %}

for gecisSayisi in range(8,0,-1) # girdiğimiz listeye göre alınan değer,
	for i in range(8)
    	# i = 1 için;
        if alist[1] > alist[2] # şart sağlanmadığı için alist[1] = 54, alist[2] = 93, 54 > 93 == False, i= 2 ye atlanır
          temp = alist[1] 
          alist[1] = alist[2] 
          alist[2] = temp
          
{% endhighlight %}

i = 1 için if şartı sağlanmıyor, bu yüzden i = 2 ye geçiyoruz.

{% highlight python %}

for gecisSayisi in range(8,0,-1) # girdiğimiz listeye göre alınan değer,
	for i in range(8)
    	# i = 2 için;
        if alist[2] > alist[3] # 
          temp = alist[2] 
          alist[2] = alist[3] 
          alist[3] = temp
#>>> temp = alist[2]
#>>> alist[2] = alist[3]
#>>> print(alist)
#[26, 54, 17, 17, 77, 31, 44, 55, 20]
#>>> alist[3] = temp
#>>> print(alist)
#[26, 54, 17, 93, 77, 31, 44, 55, 20]

#Bu geçiştede bu, nereye gittiğini görebiliyorsunuz sanırım.
          
{% endhighlight %}

i = 3 için 93 ile 77 nin yeri değişecek, 



i = 4 için 93 le 31 in, 



i = 5 için, 93 le 44 ün, 



i = 6 için 93 le 55 in ve en son 



i = 7 için 93 le 20 nin yeri değişecek.




Ve listenin üzerinden ilk geçişimizde en büyük olan sayıyı bulmuş ve listenin en sonuna atmış olduk.Şimdi ilk geçişimizi tamamladık, 7 geçiş daha yaptığımız zaman liste %100 bir ihtimalle küçükten büyüğe sıralanmış olacak.

for gecisSayisi in range(8,0,-1) # girdiğimiz listeye göre alınan değer, ilk geçişimizi tamamladığımız için gecisSayisi = 7 oluyor, for i in range(gecisSayisi) da aşağıdaki gibi oluyor.

{% highlight python %}
	for i in range(7)
    	# i = 0 için;
        if alist[0] > alist[1] # 
          temp = alist[0] 
          alist[0] = alist[1] 
          alist[0] = temp
{% endhighlight %}
Aynı şeyi tekrarlıyoruz, bu loopta:



i = 0 için birşey olmaz 26 < 54



i = 1 için 54 > 17 olduğu için 54 ile 17 yer değiştirir



i = 2 için 54 < 77 olduğu için birşey olmaz



i = 3 için 77 > 31 olduğu için yer değiştirir



i = 4 için 77 > 44 olduğu için yer değiştirir



i = 5 için 77 > 55 olduğu için yer değiştirir



i = 6 için 77 < 93 olduğu için birşey olmaz




ve listemiz
[26, 17, 54, 31, 44, 55, 20, 77, 93]

olur. Bu böyle devam edip en sonunda listemiz küçükten büyüğe doğru sıralanmış olur.

## Algoritmanın Hızı

| Geçiş Sayısı 	| Yapılan Karşılaştırma Sayısı 	|
|--------------	|------------------------------	|
| 1            	| n - 1                        	|
| 2            	| n - 2                        	|
| 3            	| n - 3                        	|
| ...          	|                              	|
| n-1          	| 1                            	|


Liste **n** büyüklüğünde olursa geçiş sayımız herzaman **n-1** büyüklüğünde olur. Karşılaştırma sayımızda _**n-1 e kadar olan bütün sayıların toplamı**_ olur tablodanda gördüğünüz gibi. 

n-1 e kadar olan bütün sayıların toplamı n-1*n-2 / 2 yani 1/2 n^2 + 1/2 n - n olur. Buda O(n^2) ye denk gelir. Algoritma yavaştır ve daha iyi sıralama yöntemleri vardır.Onlarıda ilerideki gönderilerimde anlatacağım.










