---
published: true
layout: post
title: Algoritma(V) Javascript
categories: Javascript
tags: 
- algoritma
---

Bu gönderimde bir stringin içindeki en fazla harfi olan kelimenin uzunluğunu bulma freecodecamp "challange" sini yapacağım.

problemi gayet iyi açıkladım sanırım.Direk başlıyorum : 
{% highlight js %}
function findLongestWord(str) {
  return str.length;
}
findLongestWord("The quick brown fox jumped over the lazy dog");
{% endhighlight %}
Bunu vermişler bize.Düşüncem stringi alıp arraya çevirmek.Sonrada bu arraydaki bütün elementlerin uzunluklarını bulmak, en yüksek uzunluğu bir var içinde saklamak.
{% highlight js %}
function findLongestWord(str) {
  var array = str.split(" "); // Cümledeki boşluklara göre ayırmamızı sağlıyor
}
findLongestWord("The quick brown fox jumped over the lazy dog");
{% endhighlight %}

split methodunu daha önceki gönderilemde çok kullandım.Stringi alıp array a çevirmemizi sağlıyor.Yani

"The quick brown fox jumped over the lazy dog" oluyor size ; 

["The","quick","brown","fox","jumped","over","the","lazy","dog"]
{% highlight js %}
function findLongestWord(str) {
  var array = str.split(" ");
  var kelimeUzunlugu = 0; 
  	  for(var i = 0; i< array.length;i++){ // arraydaki bütün elementleri tarıyoruz.Klasik for loopu
        if(array[i].length > kelimeUzunlugu){ // eğer array[i] deki elementin uzunluğu kelimeUzunlugu'ndan büyükse ;
          kelimeuzunlugu = array[i].length; // kelimeUzunlugu = array[i] deki elementin uzunluğu
        }
   }
  return kelimeUzunlugu; // en sonundada bu uzunluğu yolluyoruz
}
findLongestWord("The quick brown fox jumped over the lazy dog");
{% endhighlight %}
