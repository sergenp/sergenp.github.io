---
published: false
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
print(ad,yas) ##veya
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



