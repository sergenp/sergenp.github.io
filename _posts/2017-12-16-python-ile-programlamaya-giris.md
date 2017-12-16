---
published: true
layout: post
categories: Python
tags:
  - eğitim
---
# Python ile Programlamaya Giriş
### Python'u Yüklemek ve Editör
Ben anlatımlarımda Python 3.* sürümlerini temel aldığım için sizinde 3.* yüklemenizi tavsiye ederim.
Python'u indirmek için [buraya](https://www.python.org/downloads/ "Python İndirme Sayfası"),

Editör olarakta Pycharm kullanıyorum, Pycharm indirmek için [buradan](https://www.jetbrains.com/pycharm/download/#section=windows "Pycharm İndirme Sayfası") Community versiyonunu ücretsiz olarak indirebilirsiniz.
### Değişken Tanımlama
Python, yorumlayıcı bir dil olduğu değişken tanımlamak diğer dillere göre daha kolaydır. Değişkene atadığımız değere göre değişken türünü kendi tanımlar örnek olarak;
{% highlight python %}
yas=20 #tam sayı değer atadığımız için, yas'ı otomatik olarak int tanımlayacaktır.
ad="Umut" #metin değeri atadığımız için, ad'ı otomatik olarak string/char tanımlayacaktır.
{% endhighlight %}

### Ekrana Yazdırma
Ekrana yazdırmak istediğimi değer değişkense direk print(değişken_adı), bir değişken değil ise print("tırnak içerisinde") yazabiliriz örnek olarak;
{% highlight python %}
yas=20
ad="Umut"
print(ad,yas) #veya
print("Merhaba",ad)
{% endhighlight %}


### Kullanıcıdan Değer İsteme
Kullanıcıdan değer isterken, input komutunu kullanıyoruz, Python 2 versiyonlarında sayı olarak değer isterken input() komutunu, metin olarak değer isterken raw_input() komutunu kullanabilirsiniz. Ben 3 versiyonlarını örnek aldığım için yalnızca input() ile iki türlü değişkenide istetebilirsiniz, Örnek olarak;
{% highlight python %}
ad=input("Adinizi Giriniz ")
yas=input("Yasizini Giriniz ")
print(ad,yas)
{% endhighlight %}
fakat input komutuyla girdiğimiz sayılar üzerinde matematiksel işlemler yapmak için;
{% highlight python %}
dogumyili=Int(input("Doğum Yılınızı Giriniz: "))
tarih=Int(input("Şimdiki Yıl Bilgisini Giriniz: "))
yas=tarih-dogumyili
print("Yaşınız ",yas,"'dır")
{% endhighlight %}

### Matematiksel İşlemler
Direk örnekler üzerinden göstereceğim
String/Char değişkenlerde;
{% highlight python %}
a="Mer"
b="Haba"
c=a+b
print(c) #veya
print(c,"Dünya)
{% endhighlight %}
Sayılarda;
{% highlight python %}
a=5
b=10
c=a+b
d=b-a
e=a*b
f=a/b
print(c)
print(e-c)
print((a*b)-(a+b)
{% endhighlight %}
Üst ve Mod alma;
{% highlight python %}
a=3**2
print(a)
b=2**3
print(b)
c=12%2
print(c)
{% endhighlight %}
Sayıyı arttırmak
{% highlight python %}
a=5
b=7
a +=b #veya a=a+b
b +=3 #veya b=b+3
{% endhighlight %}

### Kontrol Yapısı(if-elif-else)
#### İf yapısı
If çeviri olarak "Eğer" anlamına gelir, yani belirtilen koşul doğruysa yapılacak değerleri if satırının içine yazarız. Örnek olarak;
{% highlight python %}
a=Int(input("Bir sayı giriniz: ")
if (a%2)==0:
	print("Sayı Çifttir")
{% endhighlight %}
If yapılarında dikkat edilmesi gereken yer, "**:**" parametresidir.
#### Elif yapısı
Elif çeviri olarak "eğer değilse" anlamına gelir, yani belirtilen koşul doğru değilse, elif koşulunun doğrulunu kontrol eder. Örnek olarak;
{% highlight python %}
a=11
if a%2==1:
	print("Sayı Tektir.")
elif a%2==0:
	print("Sayı Çifttir.")
{% endhighlight %}
#### Else yapısı
Else çeviri olarak "değilse" anlamına gelir, belirtilen koşul/koşullar doğru değilse else parametresi içerisinde ki işlemler yapılır. Örnek olarak;
{% highlight python %}
if (a%2)==0:
	print("Sayı Çifttir.")
else:
	print("Sayı Tektir.")
{% endhighlight %}

# Bu yazım buraya kadar, bir sonraki yazımda, döngüler, listeler ve kümeleri ele alacağım, okuduğunuz için teşekkür ederim.



