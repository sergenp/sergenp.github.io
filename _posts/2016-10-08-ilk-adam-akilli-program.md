---
published: true
layout: post
title: İlk Adam Akıllı Program(Ruby)
categories:
  - Ruby
tags:
  - ilkprogram
---
{% highlight ruby %}
puts "ilk adam akıllı program"
{% endhighlight %}
Ruby'yi yüklediğimize göre ilk adam akıllı programımızı yapabiliriz.Öyle güzel bişey beklemeyin tabii.    

Liseli bi arkadaşım bana gelip :

-
_Ya abi bize garip garip sorular soruyolar bi tanesini yapamadım ben bilgisayar mıyım_, dedi.
Ben neyi diye sorunca: 

-
_Bana 5 ten 150 ye kadar olan bütün sayıların toplamını sordular.Bende yapamadım haliyle.Bunun bi kısa yolu falan yokmu_?

Problemimiz belliydi.X den Y'ye kadar olan sayıların toplamı.Eee biz mühendis değilmiyik deyip bakalım yapabilirmiyiz böyle bi program dedim.Açtım sublime texti.

![]({{site.baseurl}}/images/ilkadamakilliprogram/getsler.png)

Kullanıcıdan 2 tane input alıyoruz.Bunlar x ve y sayılarımız(s fonksiyonu newline koymaya yarıyor hiçbi marifeti yok yazmasanızda olur sadece görsel açıdan biraz iyi gözüküyor o kadar).Buraya kadar tamam.Şimdi bizim bi şekilde x den y ye kadar olan sayıları bir yerde depolamamız lazım.En kolay seçenek bir array gibi gözüküyor.

![]({{site.baseurl}}/images/ilkadamakilliprogram/loop1.png)

i diye bir variable çıkarıp x-1 e eşitledik.Bu, örnek olarak 2'den 100 e kadar olan sayıların toplamını alıcak olursak programın 2 yi de bu toplama dahil etmesi anlamına geliyor.Sonrası basit while döngüsü.i ye den küçükken hepsi arrayına i yi ekle anlamına gelen basit bir kod.Şimdi yapmamız gereken bu arraydaki bütün i leri toplamak.

![]({{site.baseurl}}/images/ilkadamakilliprogram/loop2.png)

Ve bitiş! Bu kadar basit.
{% highlight ruby %}
for i in hepsi
    p += i
end
{% endhighlight %}
Bu kodu açıklayacak olursak. for i in hepsi satırı hepsi arrayındaki bütün elementleri bulmaya yarar. Örnek verecek olursak;

hepsi =[1,2,3,4] olursa 
i sırasıyla 
i=1, i=2, i=3, i=4 değerlerini alır.

Bu i yukarda kullandığımız i ile karıştırılmamalıdır.Bu i geçici değişken olur. i yerine herhangi bişeyde yazabilirsiniz. p += i dememiz ise i nin değerlerini p ye eklemekten ibaret. yani; 

p = 0 ile başlamıştık

i = 1 oldu. Bunu p ye ekledik ---> p = 1 oldu

i = 2 oldu. Bunu p ye ekledik ---> p = 3 oldu

i = 3 oldu. Bunu p ye ekledik ---> p = 6 oldu

i = 4 oldu. Bunu p ye ekledik ---> p = 10 oldu.

En sonundada puts #{"p"} yi kullanarak p değişkenini kullanıcıya gösterdik. Bu kadar! İlk adam akıllı programımızı yaptık. Tabiki bu programımızı geliştirebiliriz.Örneğin eğer ilk girilen sayı 1 ise bunun oklid midir gaus mudur bi adamın bulduğu (güzelim lise yıllarımı bu formüllerle harap ettim) (x * x+1) / 2 diye bi formül var.If else kullanarak bunu yazdığımız ifadeye ekleyebiliriz.

Bu arada eğer adam gelipte sayı girceği yere fsewtsdctr fln yazarsa en başta x.to_i yazdığımız kod string değerlerini 0 a dönüştürüyor.Bir if statement daha yazıp eğer x 0 sa kodu yanlış girdi vb yapabilirsiniz. Ben bunların fnin yapılmış halini şuracığa ekleyimde kalsın.
{% highlight ruby %}
def hepsini_topla
    puts ("Başlangıç tamsayısı giriniz")
    e = gets.chomp.to_i
    puts("Bitiş tamsayısı giriniz")
    a = gets.chomp.to_i
    if(e > a)
        puts "\nBaşlangıç sayısı bitiş sayısından büyük olamaz\n"
        hepsini_topla()
    elsif (e == 0 || a == 0 )
        puts "\nGirdiğiniz sayı 0 olamaz veya girdiğiniz giriş sözcük olamaz\n" # .to_i stringleri 0 sayısına çevirdiği için 0 girdisini yoksaydım
        hepsini_topla()
    elsif (e === a)
        puts "\nİki sayı birbirine eşit olmamalı\n" # <.<
        hepsini_topla()
    elsif (e === 1)
        puts "\n#{e}'den #{a}'e kadar olan tamsayıların toplamı\n(#{e} ve #{a} dahil)" # formül varken o kadar cpu kullanmaya gerek yok
        i = a + 1 # heryerde i variable kullanıyom taktım i ye herhalde
        b = a*i / 2
        puts "#{b}\n"
    else
        puts "\n#{e}'den #{a}'e kadar olan tamsayıların toplamı(#{e} ve #{a} dahil)\n" # kullanıcıya gösterelim hangi sayıları girdiğini belki unutur gerçi bunu göstermesek kullanan programın ne yaptığını bilmiycek o ayrı mesele
        hepsi = []
        i = e - 1
        while i<a do
            i += 1
            hepsi.push(i)
        end
        p=0
        for i in hepsi # hepsi.each() do |s| daha havalı ama biz böyle öğrendik başta napalım
            p += i
        end
        puts "+= " + "#{p}"
    end
    p
end
hepsini_topla
{% endhighlight %}
