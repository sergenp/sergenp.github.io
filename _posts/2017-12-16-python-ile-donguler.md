---
published: true
layout: post
categories: Eğitim
tags:
  - eğitim
  - python
  - türkçe
---
# Python ile Döngüler

## Döngüler

### While Döngüsü
While dongüsü, belirtilen koşul sağlandığı sürece, söylenen komutları yerine getirir. Örnek olarak
{%highlight python%}
a=0
while a<=10:
	print(a)
    a+=1
{%endhighlight%}
Burada "a, 10'dan küçük ve ya eşit olduğu sürece" koşulunu kullandık.

### For Döngüsü

{%highlight python%}
for karakter in "Umut-Fırat":
	print(karakter)
{%endhighlight%}
Burada karakter değişkenin içine "Umut-Fırat" kelimesinde ki her harfi tek tek atayıp ekrana yazdırıyor, kelime bittiği zaman ise döngü sonlanıyor.

#### range() fonksiyonu
range() fonksiyonu parantez içerisinde belirttiğimiz aralıktaki sayıları değişkene atayarak çalıştırır, yani döngümüzün 10 kere çalışmasını istiyorsak;
{%highlight python%}
for i range(1,10):
	print(i)
{%endhighlight%}
1 ile 10 aralığında ki sayıları ekrana yazdırdık.
#### len() fonksiyonu
len() fonksiyonu uzunluktan gelir, içine girilen string değerinin kaç karakterden oluştuğunu belirtir örnek olarak;
{%highlight python%}
ad="Umut Fırat"
print(len(ad))
{%endhighlight%}
Bu örneğimizin çıktısı 10 olacaktır, isim ve soyisim arasındaki boşluğu da karakter olarak sayıyor.
#### break ve continue deyimleri
İki deyimide örnekler üzerinden açıklayacağım;
{%highlight python%}
while true: #sonsuz döngü oluşturdum.
	kadi=input("Kullanıcı Adınızı Giriniz: ")
    sifre=input("Şifrenizi Giriniz: ")
    if (kadi=="umut")and(sifre=="123"):
    	print("Başarıyla giriş yaptınız")
        break #kullanıcı adı ve şifre doğruysa başarıyla giriş yaptınız diyerek programdan çıkacak.
    else:
    	print("Kullanıcı adınız veya Şifreniz yanlış") 
    print("tekrar deneyiniz.") #doğru değilse döngüyü devam ettirecek
{%endhighlight%}
{%highlight python%}
for sayi in range(0,20)
	if sayi%2==0:
    	print(sayi," sayı çifttir.")
        continue #sayının modu 0 ise ekrana sayı çifttir çıktısı verecek, ve sonrasında yazılan kodları yok sayarak tekrar döngüye başlayacak.
    print(sayi," sayisi tektir.")
{%endhighlight%}
