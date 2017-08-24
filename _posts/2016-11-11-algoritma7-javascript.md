---
published: true
layout: post
title: Algoritma(VII) Javascript
categories: Javascript
---
Bu gönderimde sonunu doğrula adlı freecodecamp "challange" sini yapacağım.

### Confirm the Ending (Sonunu Doğrula)

Bize demişlerki f(x,y) li bi fonksiyon yazın x'in sonu y ise true; değilse false gönderin.Tek line da yazabilceğimiz bir kod aslında.Hemen başlıyorum:
{% highlight js %}
function confirmEnding(str, target) {
  return str.substr(-target.length) === target;
}
confirmEnding("Bastian", "n");
{% endhighlight %}
Bu kadar.Açıklayalım :

.substr() methodu aynı arraydaki .split() fonksiyonuna benziyor. Şöyle örnekler verelim daha kolay anlaşılır:
{% highlight js %}
var str = "Hello world!";
var res = str.substr(1, 4);
 // res ===>>> ello
{% endhighlight %}
Veya
{% highlight js %}
var str = "Sergen";
var res = str.substr(3, 7); 
 // res ===>>> gen
{% endhighlight %}
Gibi.Eğer substr içine - koyarsak stringimizi kesmeye sondan başlar.Şunun gibi;
{% highlight js %}
var str = "Sergen";
var res = str.substr(-2); 
 // res ===>>> en
{% endhighlight %}

Peki biz ne yaptık? str.substr(-target.length) i açalım:
{% highlight js %}

confirmEnding("Bastian", "n"); // ele alalım;

str = "Bastian";

target = "n";

Bastian.substr(-"n".length )

Bastian.substr(-1) // "n".length 1 verir gördüğünüz gibi.Başınada - koyduk zaten.

Bastian.substr(-1) == n; // Yukardaki örneğimize göre

return str.substr(-target.length) === target; // dediğimizdede kısacası:

return n === target // demiş oluyoruz.

// n === n olduğu için true yolluyoruz.
{% endhighlight %}
