---
published: true
layout: post
title: Algoritma(VIII) Javascript
categories: Javascript
---

Bu gönderimde iç içe geçmiş 2 diziden en büyük numarayı bulup, diğer bir dizeye kaydetme freecodecamp "challange" sini yapacağım. 

### Return Largest Numbers in Arrays 

Verilen:

{%highlight js%}

function largestOfFour(arr) {
  return arr;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);

{%endhighlight%}

Bu 2 boyutlu arrayın üstünden geçmemizi ve arrayın içindeki her arraydan en büyük sayıyı seçip başka bir arraya kaydedip o arrayı returnlamamızı istiyolar.Direk şöyle vereyim:
{%highlight js%}

function largestOfFour(arr) {
 var enBuyukSayilar=[]; // returnlayacağımız arrayımız
  for(var i = 0;i<arr.length;i++){ // arrayı loopluyoruz
   var arrIkiEnBuyukSayi=0; // her loopda değer 0 olmalıki her ikincil arrayın en yüksek değerini doğru bulalım
    for(var j=0;j<arr[i].length;j++){ // ilk loopda arr[0][0] = 13 sonra arr[0][1] = 27 i 0 ken j bütün ikincil arrayı dönmemizi sağlıyor.
     if (arr[i][j] > arrIkiEnBuyukSayi ){ // eğer mesela arr[0][1] deki değer arrIkiEnBuyukSayi dan büyükse
      arrIkiEnBuyukSayi = arr[i][j]; // arrIkiEnBuyukSayi arr[0][1] deki değere eşitleniyor
    }
   }
   enBuyukSayilar[i] = arrIkiEnBuyukSayi; // enBuyukSayilar[0] = j loopumuz tamamlandığındaki en büyük değer
  }
  
  return enBuyukSayilar; // bütün looplar bittiğindede arrayımızı returluyoruz
}

largestOfFour([[13, 27, 18, 26], [4, 5, 1, 3], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
{%endhighlight%}
