---
published: true
layout: post
title: Algoritma(II) Javascript
categories: Javascript
tags: 
- algoritma
---

Bu gönderimde çocukluğumda en sevdiğim matematik işlemi olan faktöriyel adlı freecodecamp "challange" sini yapacağım.

### Faktöriyel!

Algoritma Challenges içindeki en kolay problem.

{% highlight js %}
function factorialize(num) {
  return num;
}

factorialize(5);
{% endhighlight %}
Böyle başlıyoruz. Kısacası girdiğimiz numun faktoriyelini bul diyolar. num! yani bulalım:

{% highlight js %}

function factorialize(num) {
  var yenisayi = 1;
  for(var i=1 ;i<=num;i++){
  yenisayi *= i;
  
  }
  return yenisayi;
}
{% endhighlight %}

Bu kadar. Kısaca açıklamak gerekirse:
{% highlight js %}
  for(var i=1 ;i<=num;i++){
  yenisayi *= i;
  }
{% endhighlight %}
i = 1 den başlıyoruz i<= num a kadar tarıyoruz.

num sayımızın 5 olduğunu kabul edersek:

i = 1 ken yenisayı = 1 --> yenisayı = i*yenisayı = 1 oluyor


i = 2 iken yenisayı = 1 --> yenisayı = i*yenisayı = 2 oluyor


i = 3 iken yenisayı = 2 --> yenisayı = i*yenisayı = 6 oluyor


i = 4 iken yenisayı = 6 --> yenisayı = i*yenisayı = 24 oluyor


i = 5 iken yenisayı = 24 --> yenisayı = i*yenisayı = 120 oluyor
