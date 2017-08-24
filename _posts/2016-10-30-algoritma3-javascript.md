---
published: true
layout: post
title: Algoritma(III) Javascript
categories: Javascript
tags: 
- algoritma
---
{% highlight js %}
function main(){
  alg3 = "Javascript ve Algoritma(I)";
  console.log(alg3);
}
{% endhighlight %}

Bu gönderimde stringi ters çevirme adlı freecodecamp "challange" sini yapacağım.

### Stringi ters çevirme

Başlık garip oldu.Bize verilen ifade şu:
{% highlight js%}

function reverseString(str) {
  return str;
}

reverseString("hello");

{% endhighlight%}

Aldığımız stringi ters çevirmemiz isteniyor. "Sergen" ---> "negreS"(güzel nick olur) gibi.
{% highlight js%}

function reverseString(str) {

   var terscevrilmisstr = '';

   }

reverseString("hello");

{% endhighlight%}
Aklıma gelen şey Stringlerde array gibi elementler içerdiği için for loop kullanıp elementlerin hepsini başka bir variable içine kaydetmek oldu.
{% highlight js%}
function reverseString(str) {

var terscevrilmisstr = '';
	for(var i = str.length-1;i >= 0; i--){
        
       terscevrilmisstr +=str[i];
        
       }
       return terscevrilmisstr;
   }

reverseString("hello");

{% endhighlight%}

Basitçe anlatayım.Girdiğimiz girdiyi alıp tersten loopluyoruz.Yani:

Girdi Sergen olsun

i değerimiz Sergen.length - 1 yani 5 olur.Arraylar bildiğiniz gibi 0 değerinden başlar.Stringlerde öyle.

i = 5 olduğu zaman ---> terscevrilmisstr += Sergen[5]; ---> terscevrilmisstr += "n";


i = 4 olduğu zaman ---> terscevrilmisstr += Sergen[4]; ---> terscevrilmisstr += "e";


i = 3 olduğu zaman ---> terscevrilmisstr += Sergen[3]; ---> terscevrilmisstr += "g";


i = 2 olduğu zaman ---> terscevrilmisstr += Sergen[2]; ---> terscevrilmisstr += "r";


i = 1 olduğu zaman ---> terscevrilmisstr += Sergen[1]; ---> terscevrilmisstr += "e";


i = 0 olduğu zaman ---> terscevrilmisstr += Sergen[0]; ---> terscevrilmisstr += "S";

Sonunda terscevrilmisstr = ""n"+"e"+"g"+"r"+"e"+"S" = "negreS" olmuş olur.
