---
published: true
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
ul.dmenu >li{ //>li yapmamın sebebi iç-içe menüde 2. oluşturacağım menünün elemanlarına etki etmesini istememem.
  float:left;
  position: relative;//pozisyonu bağıl ayarladım.
}
{%endhighlight%}
arka plan rengimi siyah ayaralayacağım ve 70 piksel boyut vereceğim.
{%highlight css%}
ul.dmenu{
  background: #000;
  height: 70px;
}
{%endhighlight%}
Yazımın rengini beyaz ayarlayacağım 32 punto yazı boyutu ve 5 piksellik beyaz bir çerçeve tanımlayacağım.
{%highlight css%}
ul.dmenu >li a{
  color:#fff; //yazı rengimi beyaz ayarlardım.
  display: block; //görüntü şeklini blok şeklinde ayarladım.
  font-size: 32pt; //yazı boyunutunu 32 punto ayarladım.
  padding:0 50px; //liste elemanlarımı blok içerisinde ortaladım.
  line-height: 70px; //yüksekliğin 70 piksel olduğunu belirtterek yazıyı dikey pozisyonda da ortaladım.
  border-right: 5px solid #fff; //ve 5 piksel boyutunda beyaz bir çerçeve ayarladım.
}
{%endhighlight%}
Şimdi 2. menümün kodlarına geçiyorum.
{%highlight css%}
ul.dmenu ul{ //ilk menümün içindeki menüler olarak tanımladım.
  background: #000; //arka plan rengini tekrar siyah olarak ayarladım.
  width: 256px; //256 piksel genişlik verdim.
  visibility: hidden; //görünebilirliğini gizli olarak ayarladım çünkü üzerine gelindiğinde açılmasını istiyorum.
  transition: 500ms all; //gerçekleşen değişikliklerde 500ms hızında olmasını istedim, animasyonlaştırdım.
  opacity: 0; //opaklığını 0 ayarladım.
  position: absolute; //pozisyonu bağımlı ayarladım, yani bağıla bağlı olarak gözükecek.
}
{%endhighlight%}
{%highlight css%}
ul.dmenu ul li{
  position: relative; //ikinci menümün pozisyonunu da bağıl olarak ayarladım.
{%endhighlight%}
Şimdi üzerine gittiğimiz zaman ikinci menümün açılmasını ve arka plan rengini değişeceğini belirtiyorum.
{%highlight css%}
ul.dmenu >li:hover >ul{ //ilk liste elemanımın üzerine gittiğimde, ikinci listemde olackaları belirtiyorum.
visibility:visible; //görünebilirliği görünür yapıyorum.
opacity:1; //opaklığı 1 ayarlıyorum.
}
ul.dmenu a:hover{
  background:#330033; //ve arka plan rengini koyu mor olarak ayarlıyorum.
}
{%endhighlight%}

## İki elemanlı dropdown(açılır) menü oluşturma kodlarınu bu şekilde. Yazımı okuduğunuz için teşekkür ederim.