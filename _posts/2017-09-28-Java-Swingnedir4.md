---
published: false
layout: post
tags: '-swing'
categories: Java
title: Java Swing(IV) - JSwing elemanları(Part 2)
---
{% highlight js %}
//JLabel,JComboBox,JCheckBox,,JTextArea,JFormattedTextField,JPasswordField (Part1)
//JRadioButton,JTextPane,JEditorPane,JSpinner,JList,JTable,JProgressBar,JScroolBar,JSlider(Part2)
{% endhighlight %}

Bu yazımda da şu kalan elemanları anlatacağım ne iş yaparlar nereye giderler falandır filandır.
Kolaylık açısından AbsoluteLayout kullanacağım.Ama bir uygulama yaparken AbsoluteLayout'u size kesinlikle tavsiye etmem.


### JRadioButton

Taa eski radyolarda bulunan bu butonlar kanal değiştirme icabı gibi birşey görürdü.Bir satırda bulunan 5 düğme olurdu, bunlardan herhangi birine basınca diğeri otomatikmen atardı.Yani aynı anda sadece bir aktif radyo butonu olabilirdi.

Ahada bu mantık tamda bizim mantığımız.

Ama bu mantığı kullanmadan önce ilk önce bize bir ButtonGroup denen java classı gerek.Bu gruba bütün JRadioButton larımızı koyacağız.
