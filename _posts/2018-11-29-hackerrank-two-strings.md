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

Çözüm ise:
{% highlight python %}
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the twoStrings function below.
def twoStrings(s1, s2):
    for i in s1:
        if i in s2:
            return "YES"
    return "NO"

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s1 = input()

        s2 = input()

        result = twoStrings(s1, s2)

        fptr.write(result + '\n')

    fptr.close()
{% endhighlight %}



