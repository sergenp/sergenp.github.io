---
published: false
layout: post
categories: Html
tags:
  - eğitim
---
## Bu yazımda, css kullanarak dropdown(açılır) menü nasıl yapılır onu anlatacağım
İlk önce Menümüzü oluşturuyoruz. Harici css kullanacağım için style.css dosyamıda siteye köprülüyorum
index.html dosyamızın kodları bu şekilde olacak;
{%highlight html%}
<html>
  <head>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <ul class="dmenu">
      <li><a href="#">Anasayfa</a></li>
      <li><a href="#">Ürünler</a>
      <ul>
        <li><a href="#">Telefonlar</a></li>
        <li><a href="#">Bilgisayarlar</a></li>
       </ul>
       </li>
      <li><a href="#">Haberler</a></li>
    </ul>
  </body>
</html>  
{%endhighlight%}
style.css dosyamızın kodları ise kademe kademe anlatacağım.
İlk olarak;
{%highlight css%}
*{ //bu etiketik içersindeki kodları sayfamın tamamına uygulayacağımı belirttim. 
list-style:none; //sırasız liste işaretini kullanmayacğaımı belirttim.
margin:0; //listemin üst girintisini 0'a eşitledim.
padding:0; //listemin soldan girintisini 0'a eşitledim.
}
{%endhighlight%}
Menü elamanlarım a etikeli ile tanımlandığından altı çizgili olacak ve ben bunu istemiyorum, o yüzden;
{%highlight css%}
a{
text-decoration:none;//yazının üzeri,üstü veya altı çizgi özelliğini kullanmayacağımı belirttim.
}
{%endhighlight%}
Menümün yatay menü olmasını istediğim için;
{%highlight css%}
ul.dmenu{
}
{%endhighlight%}
