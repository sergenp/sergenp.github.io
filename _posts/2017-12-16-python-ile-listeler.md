---
published: false
---
# Python ile Listeler
Listeler diğer programlama dillerinde ki dizilere karşılık olarak gelir.
## Liste oluşturma
Liste oluşturmak için değişkenimize [] etiketi ile değer atarız. Örnek olarak;
{%highlight python%}
liste=["umut","fırat","ile","python","öğreniyoruz"]
{%endhighlight%}
Listede ki her elemanın bir indis numarası vardır, ilk eleman 1 indis numarası ile başlar, listeden bir elemanı yazdıracağımız zaman indis numarasını girerek yazdırırız. Örnek olarak;
{%highlight python%}
liste=["umut","fırat","ile","python","öğreniyoruz"]
print(liste[0],liste[1]) #kodları ile ekrana listenin 1.ve 2. elemanlarını yazdırdık.
{%endhighlight%}