---
published: true
layout: post
title: Algoritma(I) Javascript
categories: Javascript
tags: 
- algoritma
---
{% highlight js %}
function main(){
  alg1 = "Javascript ve Algoritma(I)"
  console.log(alg1);
}
{% endhighlight %}

freeCodeCamp sitesinde gördüğüm algorithm challangesleri yapabildiğim kadarını yapıp burda paylaşmaya karar verdim belki bi işime(işinize) falan yarar.Seri şeklinde paylaşacağım büyük ihtimal.

Bütün algoritmalar challengeler(Türkçe'sini tam bulamadım zorluklar havlamak falan yazıyordu google çeviride tam anlamına gelmiyo gibime geldi.) javascript ile yapılmakta. 

### Title Case a Sentence(a.k.a Cümlenin İçerdiği Her Kelimenin İlk Harfi Büyük Olsun)

Bize fonksiyon olarak şöyle bişey vermişler;
{% highlight js %}
function titleCase(str) {
  return str;
}

titleCase("I'm a little tea pot");
{% endhighlight %}

Girdiğimiz str yi al bütün kelimeleri büyüt geri toparla diye.Yazmaya başlayalım;
{% highlight js %}
function titleCase(str) {
 var array = str.toLowerCase().split(' '); 
 return array;
}

titleCase("I'm a little tea pot");
{% endhighlight %}
Aldık stringi arraya dönüştürdük boşluklarla split ettik bütün stringi küçük harfe dönüştürdük. Arrayımız oldu 
{% highlight js %}
["i'm","a","little","tea","pot"]
{% endhighlight %}
Geldik 2.adıma for loopla arraycığımızın "item" lerinin üstünde geçicez
{% highlight js %}

function titleCase(str) {
 var array = str.toLowerCase().split(' '); 
  for (var i = 0; i< array.length; i++){
  
  }
 return array;
}

{% endhighlight %}
Bu kısım kolaydı zaten.Geldik Amerikalıların dediği gibi "Where the magic happens" kısmına:

{% highlight js %}

function titleCase(str) {
 var array = str.toLowerCase().split(' '); 
  for (var i = 0; i< array.length; i++){
   array[i] = array[i].charAt(0).toUpperCase() + array[i].slice(1); 
  }
 return array.join(' ');
}

{% endhighlight %}

Burdaki olayı kısaca açıklayayım i = 0 ken bakalım noluyor:
{% highlight js %}
array[0] = array[0].charAt(0).toUpperCase() + array[0].slice(1);
array[0]=  "i\'m" .charAt(0).toUpperCase() + "i\'m".slice(1);
array[0] = "i".toUpperCase() + "\'m"
array[0] = "I" + "\'m"
array[0] = "I\'m"
{% endhighlight %}
[String.prototype.slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice "String.prototype.slice") fonksiyonunun ne işe yaradığını öğrenmek için üstüne tıklamanız yeterli.
Bakalım 1 ken ne oluyor:
{% highlight js %}

array[1] = array[1].charAt(0).toUpperCase() + array[1].slice(1);
array[1]=  "a".charAt(0).toUpperCase() + "a".slice(1);
array[1] = "a".toUpperCase() + ''
array[1] = "A" + ' '
array[1] = "A"
{% endhighlight %}
2 iken:
{% highlight js %}

array[2] = array[2].charAt(0).toUpperCase() + array[2].slice(1);
array[2]=  "little".charAt(0).toUpperCase() + "little".slice(1);
array[2] = "l".toUpperCase() + 'ittle'
array[2] = "L" + 'ittle'
array[2] = "Little"
{% endhighlight %}
Mantığımız böyle devam ediyor.En sonunda arraymız şu hali alıyor :
{% highlight js %}
["I'm","A","Little","Tea","Pot"]
{% endhighlight %}
{% highlight js %}
array.join(' ');
{% endhighlight %}
ifademizde bu elementlerin hepsini birleştirip string e çevirmemizi sağlıyor.
{% highlight js %}
array.join(' '); // bir boşluk kullanmamızın amacı bütün array "item"lerini boşlukla ayır demek yani bunun çıktısı I'm A Little Tea Pot olur.
array.join('/') // böyle bir ifade kullansaydık çıktısı I'm/A/Little/Tea/Pot olurdu.
{% endhighlight %}
[Array.prototype.join](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join "Array.prototype.join") linkinden daha fazla bilgi alabilirsiniz.
