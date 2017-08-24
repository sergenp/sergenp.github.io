---
published: true
layout: post
title: Algoritma(IV) Javascript
categories: Javascript
tags: 
- algoritma
---
### Palindrom Bulma(a.k.a tersi ile düzü aynı; ses gibi)
Böyle başlıyoruz:
{% highlight js%}
function palindrome(str) {
  // Good luck!
  return true;
}
palindrome("eye");
{% endhighlight%}

Diyorki: "You'll need to remove all non-alphanumeric characters (punctuation, spaces and symbols) and turn everything lower case in order to check for palindromes." 

Bütün alphanumeric olmayan karakterleri girilen stringden çıkarcakmışız(direk regex geliyo tabii akla) sonra herşeyi küçük harfe dönüştürüp palindrom bakcakmışız. Geçen Algoritma(III) Javascripte yaptığım ters alma işlemini burada gerçekleştirebiliriz.
{% highlight js%}
function palindrome(str) {
  var sergn = str.toLowerCase().replace(/[\W_]+/g,"");
}
palindrome("eye");
{% endhighlight%}
[Regular Expressions(regex)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) için buraya bakabilirsiniz.Ama kısaca açıklamak gerekirse [\W] a dan z ye 0 dan 9 a bütün alphanumeric karakterleri karşılıyor. Yani [\W] = [^a-zA-Z0-9_] demek. [\W_] demek ise _ larında kaybolmasını sağlıyor. Bu ifade bütün alphanumeric karakterlerin korunmasını sağlıyor, alphanumeric olmayan karakterleride "" ile replace ediyor. Gerisi kolay zaten:
{% highlight js%}
function palindrome(str) {
  var sergn = str.toLowerCase().replace(/[\W_]+/g,"");
  var reversedstr = '';
  for(var i = sergn.length-1;i >= 0;i--){
    reversedstr += sergn[i];
  }
    if(reversedstr === sergn){
      return true;
    }  
    else{
      return false;
    }
}
palindrome("My age is 0, 0 si ega ym.");
{% endhighlight%}
