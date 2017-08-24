---
published: true
layout: post
title: Algoritma(VI) Javascript
categories: Javascript
tags: 
- algoritma
---

### Mutations
{% highlight js %}
function mutation(arr) {
  return arr;
}
mutation(["hello", "hey"]);
{% endhighlight %}

Bu algoritmada bize verilen bir arraydaki ilk elementin, ikinci elementin harflerini içeriyormu içermiyormu diye kontrol etmemiz isteniyor. 

Bize arrayın ilk iki elementi gerekiyor :
{% highlight js %}
function mutation(arr) {
  var birinci = arr[0].toLowerCase();
  var ikinci = arr[1].toLowerCase();
  }
mutation(["hello", "hey"]);
{% endhighlight %}
Haliyle. Problemde bizden büyük-küçük harfleri ihmal etmemiz söyleniyor. O yüzden .toLowerCase kullanıyoruz.
{% highlight js %}
function mutation(arr) {
  var birinci = arr[0].toLowerCase();
  var ikinci = arr[1].toLowerCase();
  for (i=0;i<ikinci.length;i++) {
    if (birinci.indexOf(ikinci[i]) < 0)
      return false;
  }
  return true;
 }
mutation(["hello", "hey"]);
{% endhighlight %}
Burayıda kısaca açıklamak gerekiyor sanırım. [indexOf() Fonkisyonu için tıklayın](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)
loopu çalıştıralım, 

mutation(["hello", "hey"]); girdiğimizi düşünelim:

i = 0 için eğer birinci.indexOf(ikinci[0]) < 0 sa false gönder. ikinci[0] = 'h'


i = 0 için eğer birinci.indexOf('h') < 0 sa false gönder.


birinci.indexOf('h') eğer 0 dan küçük bir değer veriyorsa, ki indexOf() fonksiyonu eğer bu harfi içermiyorsa -1 gönderir, bizde false gönderiyoruz, yani bu harfi içermiyor, yani birinci de ikincinin bir harfi bulunmuyor, yanlış.

Ama tabikide birinci.indexOf('h') bu durumda bize 0 değeri verir.Bu yüzdende loop devam eder:

i = 1 için eğer birinci.indexOf(ikinci[1]) < 0 sa false gönder. ikinci[1] = 'e'

i = 1 için eğer birinci.indexOf('e') < 0 sa false gönder. 
birinci.indexOf('e') bize 1 değerini verir. If statement gerçekleşmez loop devam eder;

i = 2 için eğer birinci.indexOf('y') < 0 sa false gönder. 
birinc.indexOf('y') bize -1 değerini verir.Çünkü "hello" stringi "y" harfi içermez. Bu yüzden false değeri gönderilir ve loopdan çıkılır. 

Eğer birinci string ikincide bulunan harfleri içerseydi loop tamamlanır ve looptan çıkılırdı ve hiçbişey gönderilmezdi.Bu yüzden bizde loop dışına çıktığımızda return true; yazarak birinci stringin ikincide bulunan harfleri içerdiğini söylüyoruz.
