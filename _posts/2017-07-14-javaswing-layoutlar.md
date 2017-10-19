---
published: false
title: Java Swing (V) - Layoutlar
layout: post
categories: Java
---
Başlıktanta anlaşıldığı gibi, geçen postumda da bahsetmiştim, layoutlardan bahsedeceğim. Şimdilik, javanın kaç tane layoutu var bilmiyorum. Şimdi sayıyorum açıkcası.
Layoutlar şunlardan ibaret ki geçen postumdan kopyala yapıştır yaptım:

- AbsoluteLayout
- BorderLayout
- BoxLayout
- CardLayout
- FlowLayout
- GridBagLayout
- GridLayout
- GroupLayout
- SpringLayout
- MigLayout

Belirtmek isterim ki layoutlar benim bu yazdığımdan daha fazla şeyleri yapabiliyor,yazdıklarımı sadece kısa bir özet olarak düşünebilirsiniz. 
## Absolute Layout

Geçen postumda kullandığım layout.En sevdiğim layouttur, hiçbir kısıtlaması yoktur, istediğiniz şeyi istediğiniz yere koyabilirsiniz.Bütün layoutların kendine özgü + ve - leri vardır tabikide.

Absolute layoutta hiçbirşeyin boyutu veya yeri değişmez.Yani eğer bir JFrameyi alıp büyütürseniz, butonlardır textlerdir kısacası JFrame elementleridir, hiçbirinin boyutu yeni JFrame boyutuna uyum sağlamaz ve oldukları yerde kalırlar.Yani:

<img src="/images/javaswing/javaswing5/1.gif"></img>
{% highlight java %}
frame.setLayout(null); // null layout Absolute layoutu temsil ediyor. 
{% endhighlight %}


En büyük kötülüğü budur Absolute layoutun.
Absolute layout hakkında konuşmaya fazla da gerek yok.Basit, kullanımı kolay.

## Border Layout

Border layoutta ekran North(Kuzey),East(Doğu),West(Batı),South(Güney),Center(Orta) olmak üzere ekran 5 parçaya bölünüyor.

Siz bu 5 parçaya bölünmüş ekrana tam olarak 5, evet yanlış duymadınız, tam olarak 5 tane element yerleştirebiliyosunuz.Bu istediğiniz JFrame elementi olabilir.Border layout elementlerin (x,y,width,height) özelliklerini otomatikmen bizim için ayarlıyor.Yani Absolute Layout da görülen durum bizi pek ilgilendirmiyor.

<img src="/images/javaswing/javaswing4/2.png"></img>

Bu şekilde istediğiniz elementi istediğiniz köşeye ekleyebilirsiniz.Veya daha kolayı design ı kullanın.Ben 5 buton ekledim ve JFramenin boyutunu değiştirince şöyle bir görüntü oluştu:

<img src="/images/javaswing/javaswing5/3.gif"></img>


## Box Layout
