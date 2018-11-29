---
published: false
layout: post
categories: Python
tags:
  - algoritma
---
## Hackerrank Two Strings problemi
Bizden istenilen şey eğer string 1 in içindeki herhangi bir harf string 2 nin içindeyse "YES" değilse "NO" döndermemiz.

### Çözüm
Python ile çözümü aşırı derecede kolay olduğu için bu gönderiyi yazmam bile biraz garibime gidiyor.Kısaca anlatmak gerekirse:

Python da stringler içerisinde for döngüsü ile gezebiliyoruz. Yani:
for i in "abcdefg":
	print(i) # dersek

çıktı:
a
b
c
d
e
f
g

Olur.

if "a" in "abcdefg" komutu bize "a" nın "abcdefg" de olup olmadığını True veya False döndererek bildirir. Bu if komutunda True dönderir.
if "z" in "abcdefg" -> False
if "m" in "abcskl2adm" -> True
if "az" in "azvle" -> True
if "az" in "" -> False 
... İçgüdüsel olaraktan doğrudur.


