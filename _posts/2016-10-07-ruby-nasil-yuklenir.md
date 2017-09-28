---
published: true
layout: post
title: Ruby Nasıl Yüklenir?
categories: Ruby
---
İlk gönderim ruby nasıl yüklenir hakkında olmalı diye düşündüm madem programlamaya bu dille başlıyoruz dimi? 

Linux da iseniz ruby yi yüklemek çook kolay.Terminali açıp

> _sudo apt-get install ruby_

yazdığımız an ruby yi linuxa kurmuş oluruz.Daha sonra doğru düzgün kurduğumuzu teyit etmek için

> _ruby -v_ 

yazdığımızda bir versiyon çıkıyorsa,ruby yi doğru kurduk demektir.


Geldik Windows'a

[Ruby Yükle](http://rubyinstaller.org/downloads/ "Ruby Yükle") linkinden indirebiliriz.Yükleyiciyi çalıştırdıktan sonra okla gösterdiğim yerin tikli olmasına dikkat edin.

![]({{site.baseurl}}/images/rubynasilyuklenir/rubyyukle.png)

(Evet paintlen çizdim ne var?) Yükledikten sonra cmd'ye (Win+R ye bastıktan sonra gelen kutucuğa cmd yazarsak açılan terminal benzerimsi yere) 

> _ruby -v_

> _irb -v_


yazıp versiyon doğrulaması yaptıktan sonra Ruby kullanıma hazır.

MacOSX ide anlatırdım ama malum Türkiye'de kullanan pek yok bide üşendim yazmaya bu ikisi birleşince anlatmamaya karar verdim.Hadi şimdi Hello Worldumuzu yazalım!(çok heyecanlı gerçekten,ondan ünlem varya zaten.)

Linux'ta kod yazmak hem havalı hemde herkes nedense linuxu kullandığı için(windows 10 da linux terminali kullanabiliyorsunuz bu arada.Onuda bi ara bloglarım) için bende hello worldu linuxta yazmaya karar verdim.
Meşhur programlama editoru sublime textimizi açıyoruz.Eğer sublime textiniz yoksa şu linkten indirebilirsiniz.

[Sublime Text İndir](https://www.sublimetext.com/3)

Sublime Texte şunu yazdıktan sonra:

![]({{site.baseurl}}/images/rubynasilyuklenir/ilkprogram.png)

ctrl+s yapıp sergen.rb olarak masaüstüne kaydederseniz(terminali masaüstünde açmak için masaüstünüze sağ tıklayıp uç birimde açı seçin, boşuna cd Masaüstü yazma zahmetine girmeyin) ve terminale şunu yazarsanız 

![]({{site.baseurl}}/images/rubynasilyuklenir/terminalruby.png) 

Hello Worldumuzun çıktığını görürsünüz!

Ruby için bütün basit aletlerimiz var.Bende güzel şeyler öğrendikçe sizlerle paylaşmaya devam edicem.
