---
published: false
layout: post
tags: '-swing'
categories: Java
title: Java Swing(IV) - JSwing elemanları(Part 2)
---
{% highlight java %}
//JLabel,JComboBox,JCheckBox,,JTextArea,JFormattedTextField,JPasswordField (Part1)
//JRadioButton,JTextPane,JEditorPane,JSpinner,JList,JTable,JProgressBar,JScroolBar,JSlider(Part2)
{% endhighlight %}

Bu yazımda da şu kalan elemanları anlatacağım ne iş yaparlar nereye giderler falandır filandır.
Kolaylık açısından AbsoluteLayout kullanacağım.Ama bir uygulama yaparken AbsoluteLayout'u size kesinlikle tavsiye etmem.


### JRadioButton

Taa eski radyolarda bulunan bu butonlar kanal değiştirme icabı gibi birşey görürdü.Bir satırda bulunan 5 düğme olurdu, bunlardan herhangi birine basınca diğeri otomatikmen atardı.Yani aynı anda sadece bir aktif radyo butonu olabilirdi.

Ahada bu mantık tamda bizim mantığımız.

Ama bu mantığı kullanmadan önce ilk önce bize bir ButtonGroup denen java classı gerek.Bu gruba bütün JRadioButton larımızı koyacağız.

{%highlight java%}
private void initialize() {
	frame = new JFrame();
	frame.setBounds(100, 100, 450, 300);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	frame.getContentPane().setLayout(null);
		
	JRadioButton radyoButonu1 = new JRadioButton("Kuş");
	radyoButonu1.setBounds(10, 0, 100, 25);
	frame.getContentPane().add(radyoButonu1);
		
	JRadioButton radyoButonu2 = new JRadioButton("Timsah");
	radyoButonu2.setBounds(10, 25, 100, 25);
	frame.getContentPane().add(radyoButonu2);
		
	JRadioButton radyoButonu3 = new JRadioButton("Ejderha");
	radyoButonu3.setBounds(10, 50, 100, 25);
	frame.getContentPane().add(radyoButonu3);
		
	JRadioButton radyoButonu4 = new JRadioButton("Penguen");
	radyoButonu4.setBounds(10, 75, 100, 25);
	frame.getContentPane().add(radyoButonu4);
		
	ButtonGroup group = new ButtonGroup();
	group.add(radyoButonu1);
	group.add(radyoButonu2);
	group.add(radyoButonu3);
	group.add(radyoButonu4);
}
{%endhighlight%}
<img src="/images/javaswing/javaswing4/1.gif" />
Artık bunlara bi işlevsellik ekleyebiliriz.Mesela herhangi birini seçtiğimizde bize değişik resimler versin.ActionListeneri hatırlarsınız.Onu implement ediyoruz.

{%highlight java%}
	radyoButonu1.addActionListener(this);
	radyoButonu2.addActionListener(this);
	radyoButonu3.addActionListener(this);
	radyoButonu4.addActionListener(this);
    JLabel resimLabel = new JLabel();
	resimLabel.setBounds(174, 36, 200, 150);
	frame.getContentPane().add(resimLabel);
{%endhighlight%}
Resimlerimizi tutmak için de 200x150 genişliğinde bir JLabel ekledim

Hiçbir butonumuza ActionCommand eklemediğimiz için, varsayılan ActionCommand ları Butonumuzun Text içeriği olur.Yani:
{%highlight java%}
radyoButonu1.getActionCommand() == "Kuş";
radyoButonu2.getActionCommand() == "Timsah";
.
.
.
{%endhighlight%}
Yapmamız gereken radyoButonundan actionCommandı alıp, resimLabelimizin iconunu aldığımız komutun resmine çevirmek.
resimLabel.setIcon() komutuyla resmimizi yerleştirebiliriz.
{%highlight java%}
	@Override
	public void actionPerformed(ActionEvent arg0) {
		switch(arg0.getActionCommand()) {
			case "Timsah":
	        	resimLabel.setIcon(new ImageIcon(Main.class.getResource("/main/timsah.jpg")));
	        	break;
			case "Kuş":
	        	resimLabel.setIcon(new ImageIcon(Main.class.getResource("/main/kus.jpg")));
				break;
			case "Ejderha":
	        	resimLabel.setIcon(new ImageIcon(Main.class.getResource("/main/ejderha.jpg")));
				break;
			case "Penguen":
	        	resimLabel.setIcon(new ImageIcon(Main.class.getResource("/main/penguen.jpg")));
				break;
			default:
				break;
		}
	}
{%endhighlight%}
<img src="/images/javaswing/javaswing4/2.gif" />


### JTextPane ve JEditorPane

Bahsetmeye gerek duymuyorum. JTextPane JEditorPanenin gelişmiş versiyonu diyebiliriz.Zaten ilk yazımda JTextPane kullanmıştım. Şurda farklarını anlatan çok güzel bir soru-cevap gerçekleşmiş:
[JTextPane vs JEditorPane](https://stackoverflow.com/questions/19093851/jeditorpane-vs-jtextpane)

### JSpinner
