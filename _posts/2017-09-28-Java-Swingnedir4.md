---
published: true
layout: post
tags: '-swing'
categories: Java
title: Java Swing(IV) - JSwing elemanları(Part 2)
---
{% highlight java %}
//JLabel,JComboBox,JCheckBox,,JTextArea,JFormattedTextField,JPasswordField (Part1)
//JRadioButton,JTextPane,JEditorPane,JSpinner,JList,JTable,JProgressBar,JScrollPane,JSlider(Part2)
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

JComboBox u hatırlarsınız. Temelde aynı şeyler. Açıkcası hiç kullanmadım. Her zaman JComboBox kullandım. Aralarında pek fark yok zaten.Ama buradan daha fazla bilgi alabilirsiniz.
[JSpinner](http://docs.oracle.com/javase/tutorial/uiswing/components/spinner.html)

### JList

JList gerçekten güzel bir icat.Kullanmak için, ilk önce bir model listesi hazırlıyorsunuz.Bu model listesine istediğiniz türden şeyi koyma hakkınız var.Görsel olarak anlatmak daha kolay tabii:

{%highlight java%}
JList<String> list = new JList<String>();
list.setModel(new AbstractListModel<String>() {
	String[] values = new String[] {"sergen", "ahmet", "mehmet", "abdullah", "fatma", "yurdanur", "isim", "haf\u0131zam", "bitti", "resmen", "benden", "bu", "kadar"};
	public int getSize() {
		return values.length;
	}
	public String getElementAt(int index) {
		return values[index];
	}
});
list.setBounds(10, 10, 100, 240);
frame.getContentPane().add(list);

// rastgele bir textPane, list ile etkileşime geçmesi için
textPane = new JTextPane();
textPane.setEnabled(false);
textPane.setEditable(false);
textPane.setBounds(178, 59, 113, 20);
frame.getContentPane().add(textPane);

list.addListSelectionListener(new ListSelectionListener() {
	public void valueChanged(ListSelectionEvent arg0) {
		textPane.setText(list.getSelectedValue());
	}
}); 
}
{%endhighlight%}
<img src="/images/javaswing/javaswing4/3.gif" />
___ListSelectionListener___ interfacemiz listteki herhangi bir elementi seçtiğimizde tetikleniyor.Böylelikle listteki herhangi bir elemanı seçtiğimiz de textPane mizin Text i o elemanın text ine eşit oluyor.

Burdan gördüğünüz üzere listemizden seçtiğimiz herhangi bir elementle bütün JPaneli kontrol edebiliriz.

Örnek bir isim seçtiğimizde bu isimle ilgili bilgileri ekrana yazdırabiliriz.
Veya JList modelini ImageIcon olarak alıp, herhangi bir elemana tıkladığımızda başka bir elemanın resmini değiştirebiliriz.
Veya JList modelini String olarak alıp, O stringe çift tıkladığımızda bir müzik dosyasının açılmasını sağlayabiliriz!
(MP3 player tarzında, ki github hesabımda bulabilirsiniz. [MP3 Player](https://github.com/sergenp/Minimal-Java-Projects/tree/master/mp3Player) Herhangi bir eklentiyi hoşnutlukla karşılarım.)

### JTable

Böyle birşey yapabiliriz:
{%highlight java%}
table = new JTable();
table.setBorder(new LineBorder(new Color(0, 0, 0)));
table.setModel(new DefaultTableModel(
	new Object[][] {
		{"sergen", "pek\u015Fen", "00000000000"},
		{"mahmut", "yanyatan", "00000000000"},
		{"rudik", "ulutur", "00000000000"},
	},
	new String[] {
		"\u0130sim", "Soyisim", "TelNo"
	}
));
table.setBounds(10, 10, 250, 48);
{%endhighlight%}
Sonuç:
<img src="/images/javaswing/javaswing4/4.png" />

Kısacası resmen bir excel tablosu.Databasenize birşey göndermek amaçlı kullanılabilir, veya bir yönetim yazılımı yapıp, kullanıcı bilgilerini toplamak adına bir table oluşturabilirsiniz.Böyle şeyler de kullanılabilir.

### JProgressBar

Hepimiz elbet birşey yüklemişizdir.O şeyi yüklerken dolan bir çubuk var, işte bu çubuğa ProgressBar diyolar.

ProgressBar kullanmak için genellikle main thread imiz dışında başka bir threadle çalışmak durumundayız.En azından ben böyle yapıyorum.
{%highlight java%}
progressBar = new JProgressBar();
progressBar.setBounds(109, 71, 255, 14);
frame.getContentPane().add(progressBar);

JButton basla = new JButton("Ba\u015Fla");
basla.setBounds(10, 62, 89, 23);
basla.addActionListener(new ActionListener() {
	@Override
	public void actionPerformed(ActionEvent arg0) {
		basla.setEnabled(false);
		baslat();
	}
});
{%endhighlight%}
Burdaki baslat fonksiyonumuz yeni bir thread başlatıcak, progress barımıza rastgele sayılar atıyacak, ve atanan sayı 100 den büyük olduğu zaman durduracak.

{%highlight java%}
private Thread progressThread = null;
{%endhighlight%}
Classımızın başına koyduğumuz (Instance variable) ile işimizi görmemiz gerekecek.
{%highlight java%}

public void baslat() {
	progressThread = new Thread(new Runnable() {
	// baslat methodu ilk çağırıldığında sürecimiz 0 olmalı.
		int surec = 0;
		@Override
		public void run() {
	// sürecimiz 100 den küçükken
			while(surec < 100) {
				try {
		// rastgele bir sayı oluşturmak için Random classımızı kulanmamız gerekiyor.
					Random rand = new Random();
					int  n = rand.nextInt(10) + 1; // 1,10 arası rastgele bir sayı.
					surec += n; // Her loop umuzda surec int imiz 1 ila 10 arası artıyor.
					progressBar.setValue(surec); // bu sürecide progress bar valuesi olarak atıyoruz.
					Thread.sleep(500); // sonunda Threadimizi 0.5 saniye uyutuyoruz, yani teknik olarak while loopumuzu her 0.5 saniyede bir çalıştırıyoruz.
				} catch (InterruptedException e) {
					return;
				}

			}
		}
	});
	// en sonunda bu threadi başlatmamız gerekiyor.Bunuda bu şekilde yapıyoruz
	progressThread.start();
}
{%endhighlight%}

Sonucumuz şöyle birşey oluyor:
<img src="/images/javaswing/javaswing4/5.gif" />
[Buradan Thread'e bakabilirsiniz.](http://tutorials.jenkov.com/java-concurrency/creating-and-starting-threads.html)

### JScrollPane

JScrollPane denen şey, websitelerinde gezerken çok rastlarsınız, bir "Bar"ı kaydırdığımızda sayfanın da onla birlikte kaymasını sağlayan şeydir.Genellikle çok kullanışlı olurlar.Mesela bir günlük uygulaması yaptığımızı düşünelim.JTextArea mize o kadar çok yazı yazdık ki doldu taştı ve yazdığımız yazıların yarısını göremiyoruz.Bu TextArea mize ScrollBar eklersek, TextArea mizi kaydırabilir ve görmediğimiz yerleri görebiliriz.Örneklerle daha iyi anlatırım bence
{%highlight java%}
JTextArea textArea = new JTextArea();
textArea.setLineWrap(true);

JScrollPane Jspane = new JScrollPane(textArea);
Jspane.setBounds(10, 11, 120, 65);

frame.getContentPane().add(Jspane);
{%endhighlight%}
Gördüğünüz gibi ScrollPane eklediğimiz elemanı "frame" e eklemiyoruz, ScrollPane nin kendisini ekliyoruz, bunu yaptığımızda otomatikmen zaten o elemanda eklenmiş oluyor. Yani JTextArea burda, ScrollPane'nin "Child" ı oluyor.Ve bu kod böyle çalışıyor:
<img src="/images/javaswing/javaswing4/6.gif" />

### JSlider

JSliderlar ise size bir "Bar" veriyor, onu yukarı aşağı kaydırdığınız zaman da bir "value" veriyor.Mesela bilgisayarınızın sesini açıp kapattığınızda kullandığınız elemanlar Slider olarak adlandırılıyor.

{%highlight java%}
JSlider slider = new JSlider();
slider.setOrientation(SwingConstants.VERTICAL);
slider.setBounds(10, 11, 26, 239);
frame.getContentPane().add(slider);

JLabel lblNewLabel = new JLabel("");
lblNewLabel.setHorizontalAlignment(SwingConstants.RIGHT);
lblNewLabel.setBounds(46, 83, 62, 69);
frame.getContentPane().add(lblNewLabel);
lblNewLabel.setText(String.format("%d",slider.getValue()));

// ChangeListener == Değişim Dinleyicisi
slider.addChangeListener(new ChangeListener() {
	@Override
	public void stateChanged(ChangeEvent arg0) {
		lblNewLabel.setText(String.format("%d",slider.getValue()));
	}
});
{%endhighlight%}
<img src="/images/javaswing/javaswing4/7.gif" />
