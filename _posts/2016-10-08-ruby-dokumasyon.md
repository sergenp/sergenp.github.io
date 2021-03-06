---
published: true
layout: post
title: Ruby Dökümanları
categories: Ruby
tags:
 - youtube
---
{% highlight ruby %}
def ruby
    puts "ruby ne güzel değil mi"
end
{% endhighlight %}
Bu gönderimde Ruby öğrenmek , geliştirmek vb. ile ilgili bazı kaynaklar paylaşacağım.Kaynakların hepsi ingilizce onu baştan söyleyeyim.

## İlk olarak Youtube Tutorialleri 

Youtube'de milyonlarca Ruby tutoriali var(milyonlarca değil tabide bayaa var) bazıları gerçekten çok iyi yurt dışında düzenlenen konferansların videolarını falan koyuyolar bazıları seçtim içlerinden buraya bırakıyorum resimlere tıklayarak videolara ulaşabilirsiniz;

### Ruby ile Oyun Yapmak

Ruby'de oyun yapmak için Gosu library kullanıyor arkadaşımız.Gosu library çok küçük bir Ruby library. Çok az ama yararlı biçok class içeriyor.

<iframe src="https://www.youtube.com/embed/jJhbpY70miE" frameborder="0" allowfullscreen></iframe>

Örneğin:
{% highlight ruby %} 
class oyun < Gosu::Window 
def initialize width : 800 height : 640 fullscreen = false
	super
end
oyun.new.show
{% endhighlight %} 

yazarak bir ekran oluşturabilirsiniz.
<iframe src="https://www.youtube.com/embed/H5_Kid3hpRs" frameborder="0" allowfullscreen></iframe>

Burdaki arkadaşımız hangi library kullanabilirsiniz vb. şeyleri kısa bi şekilde anlatmış.Eğer oyun yapımına ilginiz varsa mutlaka bakmanız gereken bir konferans.Ruby harici birkaç libraryde anlatıma dahil.

### Ruby Youtube Tutorials

Tabii ruby tutorials derken Derek Banas'ı es geçmemek lazım.Hakkımda bölümünde kanalını paylaştığım abimiz gerçekten işinin ehli bi insan. Sırf Ruby değil diğer dillerdede baya yardımcı oldu kendisi bana.Kesinlikle tavsiye ediyorum.

<iframe src="https://www.youtube.com/embed/Dji9ALCgfpM" frameborder="0" allowfullscreen></iframe>

Ruby tips-tricks.İşe yarar bir video.

<iframe src="https://www.youtube.com/embed/gIEMKOI_Y-4" frameborder="0" allowfullscreen></iframe>

Bu videoda Ruby sembollerini güzel bir şekilde açıklıyor.

<iframe src="https://www.youtube.com/embed/mBXGBbEbXZY" frameborder="0" allowfullscreen></iframe>

## İkinci olarak Websiteleri

Öncelikle [GitHub](github.com) tabiki. Söylemeye bile gerek yoktu ama dursun orda nolcak.Bir liste yapayım çünkü bütün siteleri açıklamak için yeterlik vaktim yok şuan için.Başlayalım:

1 - [21 Ruby Tricks](http://www.rubyinside.com/21-ruby-tricks-902.html)


2 - [10 Ruby Tricks to improve your code](https://samurails.com/ruby/ruby-tricks-improve-code/)


3 - [Best Ruby](https://github.com/franzejr/best-ruby)


4 - [Ruby Quick Tips](http://rubyquicktips.com/)


5 - [Ruby Tips and Practices](https://www.toptal.com/ruby/tips-and-practices)


6 - [Ruby Quickstart](https://www.ruby-lang.org/en/documentation/quickstart) # Ruby in 20 Minutes başlangıç için çok uygun 


7 - [Got 15 minutes? Give Ruby a shot right now!]( http://tryruby.org/levels/1/challenges/0) # Ruby'yi browserinizde denemenizi sağlıyor


8 - [Codecademy Ruby](https://www.codecademy.com/learn/ruby) # Bir süre önceye kadar bedavaydı site. Bu siteden sağolsunlar Javascript-Html-Css-JQuery-Bootstrap öğrendim. Eğer belli bir ücret verirseniz($19.99/aylık) daha iyi eğitimlere erişebilirsiniz. Şahsen ben vermem ama sizin bileceğiniz iş tabii siteyi severseniz artık. 

Şimdilik bu kadar döküman yeter herhalde. Daha sonra buldukça bu gönderiyi güncellerim artık.
