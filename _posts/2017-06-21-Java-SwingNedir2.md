---
published: true
title: 'Java Swing nedir? (II) - JFrame,JButton,JTextField'
layout: post
categories: Java
---
Bu gönderimde JFrame JButton ve JTextfield ile yapabileceğiniz küçük şeyleri anlatacağım.

#### JFrame
İlk öncelikle JFrame hakkında 2,3 şey söylemek gerek. JFrame basitçe bizim butonlarımızın, textfieldlerimizin ve bunlar gibi daha birçok şeyin bulunduğu bir "placeholder"(yer tutucu) diyebiliriz.

Bizim Main classımız şu anda bu şekilde:

{% highlight java %}
package ornek;

import java.awt.EventQueue;
import javax.swing.JFrame;

public class Main {

	private JFrame frame;
    
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Main window = new Main();
					window.frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}
	public Main() {
		initialize();
	}
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 450, 300);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	}
}

{% endhighlight %}
Burdaki:
{% highlight java %}
	public Main() {
		initialize();
	}
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 450, 300);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	}
{% endhighlight %}

Kısmımız ne zaman bir Main classı oluşturursak

{% highlight java %}
frame = new JFrame(); // yeni bir JFrame oluştur
{% endhighlight %}
{% highlight java %}
frame.setBounds(100, 100, 450, 300); // JFrame yi (xpozisyonu,ypozisyonu,yukseklik,genislik) olarak ekranımıza sabitle
{% endhighlight %}

{% highlight java %}
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // JFrameyi kapattığımızda bütün programı kapat
{% endhighlight %}

Demekten ibaret.

{% highlight java %}
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Main window = new Main();
					window.frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}
{% endhighlight %}

Java dosyamızıda compile edip çalıştırdığımızda, 
{% highlight java %}
Main window = new Main(); // yeni bir Main classı oluştur
{% endhighlight %}
{% highlight java %}
window.frame.setVisible(true); // window.frame (yani Main classın içindeki JFrame) i görünür yap.
{% endhighlight %}
Ve programımızı çalıştırdığımızda JFramemiz Ekranımızda istediğimiz pozisyonda ve büyüklükte açılmış bir şekilde karşımıza çıkar.

<img src="/images/javaswing/javaswing2/1.png" width="807" height="636" />
<img src="/images/javaswing/javaswing2/2.png" width="807" height="636" />

Tabikide açılan JFramemizde hiçbirşey yok, Peki nasıl birşeyler ekleyebiliriz?


##### JFrame ve elemanları 

Başlık "Thomas ve arkadaşları" gibi bişey oldu ama, yinede kabulum.Aslında JFrameye eleman eklemek çok kolay! Eclipsenin alt tarafında "Source" ve "Design" isimli 2 tane buton var. Source dediğimiz button güzelimsi ve okunaklı kodumuzu bize gösteriyor, Design butonuna tıkladığımızda ise karşımıza birsürü Swing elemanı çıkıyor.JFrameye eleman eklemek, bu elementleri çekip bırakmaktan başka birşey gerektirmiyor.İşin güzel tarafı ne zaman bir eleman eklerseniz bütün kodlar otomatikmen Main classımıza geliyor. 

<img src="/images/javaswing/javaswing2/3.png" width="807" height="636" />

Zaten milyon tane program kullandığınız için, bu elemanlar çok tanıdık gelmeli.Bütün hepsini anlatmak isterdim ama çok zahmetli, yaparken öğreniriz elbet.Ben basitlik açısından, bir Buton ve bir TextField ile ne yapabileceğimizi göstereceğim.

##### JFrame Layout

Layout kısaca düzen gibi birşey.Çeşit çeşit layoutlarımız var,

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

gibi.Ben bu post da AbsoluteLayout kullanacağım.
<img src="/images/javaswing/javaswing2/5.gif" width="807" height="636" />
Gördüğünüz gibi AbsoluteLayout elemanları koyacağımız yerlere karışmıyor, eğer başka layoutlar kullansaydık layoutun kendisine göre elemanları koyabileceğimiz yerler kısıtlanırdı.(Şu gifi yapmak blogu yazmaktan uzun sürdü valla)


#### JButton ve JTextField

<img src="/images/javaswing/javaswing2/4.png" width="807" height="636" />

Bir buton 2 de TextField koyduk, ve TextFieldin birinin editable kısmını false yaptım, çünkü içine birşey girilmesini istemiyorum.

TextField'e girdiğimiz String değerini alıp, diğer TextField'e tersini yazan bişey yapmak geldi.Javascript algoritmada yapmıştık eğer ona bakmışsanız. (Hangisi olduğunu hatırlamıyorum, bakmayada üşendim) 

Bastık sourcemize:
<img src="/images/javaswing/javaswing2/6.png" width="807" height="636" />

Ve otomatik eklenen kodlarla karşı karşıyayız.Şimdi o butona bir listener(dinleyici) eklememiz gerek, dinleyiciler çeşitli olayları, örneğin mouse ile basıldı, klavyeden bi tuşa bastı, mouse ile üstüne gelinildi gibi şeyleri takip etmekle yükümlü fonksiyonlar.Ben butonuma actionListener ekleyeceğim, üstüne mouse ile basıldığında olmasını istediğim şeyleri yaptıracağım.
<img src="/images/javaswing/javaswing2/7.png" width="807" height="636" />
<img src="/images/javaswing/javaswing2/8.png" width="807" height="636" />
<img src="/images/javaswing/javaswing2/9.png" width="807" height="636" />

ActionListener ide eklemiş olduk.Gelelim kod kısmımıza.


{% highlight java %}
JButton btnNewButton = new JButton("Bana Bas");
btnNewButton.setBounds(258, 50, 126, 40);
frame.getContentPane().add(btnNewButton);
btnNewButton.addActionListener(this);
btnNewButton.setActionCommand("cevir"); // ActionListener implementlediğimizde yeni bir fonksiyon gelmişti.
{% endhighlight %}

{% highlight java %}
@Override
public void actionPerformed(ActionEvent e) {
	if(e.getActionCommand() == "cevir"){ /* eğer ActionListenerden gelen command(setActionCommand ile 												* sağladığımız command) cevir e eşitse şunları yap */
    }
}
{% endhighlight %}

Peki ne yapmamız gerek? İlk koyduğumuz TextField'e girilen text i almamız lazım
{% highlight java %}
public void actionPerformed(ActionEvent e) {
	if(e.getActionCommand() == "cevir"){ 
    	String girilenString = textField.getText();
        String tersCevrilmis = tersCevir(girilenString);
        // şimdi bir Stringi tersine döndüren bir Java fonksiyonu yazalım
        
    }
}
{% endhighlight %}

{% highlight java %}
// bir String alıp bir String geri vermemiz lazım böyle bişey yani:
public String tersCevir(String girilenString){
	return new StringBuilder(girilenString).reverse().toString();
}
// Ahanda bu kadar kolay girdiğimiz string ters çevrildi.

{% endhighlight %}

Şimdide ters çevirdiğimiz stringi alıp diğer oluşturduğumuz textField_1 e kayıt etmekte

{% highlight java %}
public void actionPerformed(ActionEvent e) {
	if(e.getActionCommand() == "cevir"){ 
    	String girilenString = textField.getText();
        String tersCevrilmis = tersCevir(girilenString);
        textField_1.setText(tersCevrilmis);        
    }
}
{% endhighlight %}
<img src="/images/javaswing/javaswing2/10.png" width="807" height="636" />

ve Programımız bitmiş bulunmakta. Programımıza bir title ve icon ekleyelim.Constructor umuza gelelim

{% highlight java %}
private void initialize() {
	frame = new JFrame();
	frame.setBounds(100, 100, 450, 300);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	frame.getContentPane().setLayout(null);
    // setTitle ile Programın başlığı geliyor
	frame.setTitle("String ters çevirici");
    // setIconImage ile de JFramemizin iconunu belirliyoruz.
	frame.setIconImage(new ImageIcon(Main.class.getResource("icon.png")).getImage());
    // tabii bu icon.png'yi Main.class ımızın olduğu klasöre atmamız gerek.
    
	JButton btnNewButton = new JButton("Bana Bas");
	btnNewButton.setBounds(258, 50, 126, 40);
	frame.getContentPane().add(btnNewButton);
	btnNewButton.addActionListener(this);
	btnNewButton.setActionCommand("cevir");
		
	textField = new JTextField();
	textField.setBounds(64, 50, 126, 40);
	frame.getContentPane().add(textField);
	textField.setColumns(10);
		
	textField_1 = new JTextField();
	textField_1.setEditable(false);
	textField_1.setColumns(10);
	textField_1.setBounds(155, 133, 126, 40);
	frame.getContentPane().add(textField_1);
{% endhighlight %}
icon.png yi şöyle atabilirsiniz:
<img src="/images/javaswing/javaswing2/12.gif" width="807" height="636" />

Ve programımızın bitmiş hali:
<img src="/images/javaswing/javaswing2/13.png" width="807" height="636" />

Ve son kodumuz:

{% highlight java %}
package ornek;

import java.awt.EventQueue;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JFrame;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JTextField;

public class Main implements ActionListener {

	private JFrame frame;
	private JTextField textField;
	private JTextField textField_1;

	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Main window = new Main();
					window.frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	public Main() {
		initialize();
	}

	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 450, 300);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.getContentPane().setLayout(null);
		frame.setTitle("String ters çevirici");
		frame.setIconImage(new ImageIcon(Main.class.getResource("icon.png")).getImage());
		
		JButton btnNewButton = new JButton("Bana Bas");
		btnNewButton.setBounds(258, 50, 126, 40);
		frame.getContentPane().add(btnNewButton);
		btnNewButton.addActionListener(this);
		btnNewButton.setActionCommand("cevir");
		
		textField = new JTextField();
		textField.setBounds(64, 50, 126, 40);
		frame.getContentPane().add(textField);
		textField.setColumns(10);
		
		textField_1 = new JTextField();
		textField_1.setEditable(false);
		textField_1.setColumns(10);
		textField_1.setBounds(155, 133, 126, 40);
		frame.getContentPane().add(textField_1);
		
	}

	@Override
	public void actionPerformed(ActionEvent e) {
		if(e.getActionCommand() == "cevir"){
	    	String girilenString = textField.getText();
	    	String tersCevrilmis = tersCevir(girilenString);
	    	textField_1.setText(tersCevrilmis);
	    }
	}

	public String tersCevir(String girilenString) {
		return new StringBuilder(girilenString).reverse().toString();
	}
}
{% endhighlight %}
