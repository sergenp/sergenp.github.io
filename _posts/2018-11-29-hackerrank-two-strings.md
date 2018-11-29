---
published: true
layout: post
categories: Python
tags:
  - algoritma
title: Hackerrank - Two String
---
## Hackerrank Two Strings problemi
Bizden istenilen şey eğer string 1 in içindeki herhangi bir harf string 2 nin içindeyse "YES" değilse "NO" döndermemiz.

### Çözüm
Python ile çözümü aşırı derecede kolay olduğu için bu gönderiyi yazmam bile biraz garibime gidiyor.Kısaca anlatmak gerekirse:

Python da stringler içerisinde for döngüsü ile gezebiliyoruz. Yani:

{% highlight python %}
for i in "abcdefg":
	print(i) # dersek
{% endhighlight %}

çıktı:

a

b

c

d

e

f

g

Olur.

"a" in "abcdefg" komutu bize "a" nın "abcdefg" de olup olmadığını True veya False döndererek bildirir. Bu komut True dönderir.

{% highlight python %}
"z" in "abcdefg" #-> False
"m" in "abcskl2adm" #-> True
"az" in "azvle" #-> True
"az" in "avlez" #-> False
"az" in "" #-> False 
{% endhighlight %}

Çözüm ise:
{% highlight python %}
def twoStrings(s1, s2):
    for i in s1:
        if i in s2:
            return "YES"
    return "NO"

print(twoStrings("random", "strings")) # "YES" -> iki stringin içindede r var
print(twoStrings("rank", "false")) # "YES" -> iki stringin içindede a var
print(twoStrings("bir", "üç")) # "NO" -> iki stringin içinde ortak bir harf yok

{% endhighlight %}

