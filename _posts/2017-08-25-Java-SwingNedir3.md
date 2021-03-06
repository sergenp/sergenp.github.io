---
published: true
layout: post
title: Java Swing(III) - JSwing elemanları(Part 1)
category: Java
tags:
  - swing
---
{%highlight java%}
//JLabel,JComboBox,JCheckBox,,JTextArea,JFormattedTextField,JPasswordField (Part1)
//JRadioButton,JTextPane,JEditorPane,JSpinner,JList,JTable,JProgressBar,JScroolPane,JSlider(Part2)
{%endhighlight%}
Hah, "Swing components" lerden kalan yukarıda yazanlarıda bu yazıda halledelim.

Bu yazıda çekirdek olarak şöyle bir kodla başladığımızı farzediyorum, ve eklediğim şeyler genellikle initalize() altında olacak:
{%highlight java%}
private JFrame frame;
/**
 * Launch the application.
 */
public static void main(String[] args) {
	EventQueue.invokeLater(new Runnable() {
		public void run() {
			try {
				JSwingElemanlar window = new JSwingElemanlar();
				window.frame.setVisible(true);
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	});
}

/**
 * Create the application.
 */
public JSwingElemanlar() {
	initialize();
}
private void initialize() {
	frame = new JFrame();
	frame.setBounds(100, 100, 450, 300);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
{%endhighlight%}
### JLabel

Label, adı üstünde etiket, bu güzel kolay kullanımlı elemanımız, etiketlemeye yarıyor.
Etiketi bir resimle, sadece yazıyla veya sadece resimle kullanabilirsiniz.

{%highlight java%}
frame = new JFrame();
frame.setBounds(100, 100, 450, 300);
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.getContentPane().setLayout(new GridLayout(3, 1, 0, 0));
// gridlayout kullanıyorum,
// kendisi güzeldir baya, elbet bir yazımızda ondan da bahsederiz.
ImageIcon resim =  new ImageIcon(
	Main.class.getResource("/javax/swing/plaf/basic/icons/JavaCup16.png")
	); // javanın kendi resmini arakladım
JLabel etiket1 = new JLabel("Resim ve Yazı",
	 resim,
	 JLabel.CENTER);
//etiketimizi iconumuzun olduğu konuma göre yerini belirliyoruz.
//resmimiz ve yazımızı bir kare olarak düşünürsek, 
etiket1.setVerticalTextPosition(JLabel.BOTTOM); // dikey olarak karemizin en altına
etiket1.setHorizontalTextPosition(JLabel.CENTER); // yatay olarak karemizin ortasına
// konumlandırmış oluyoruz yazımızı

JLabel etiket2 = new JLabel("Sadece Yazı"); // sadece yazılı bir etiket
JLabel etiket3 = new JLabel(resim,JLabel.CENTER);  // sadece resimli bir etiket
frame.getContentPane().add(etiket1);
frame.getContentPane().add(etiket2);
frame.getContentPane().add(etiket3);

{%endhighlight%}
Yukarıdaki kodumuzun sonucu şöyle birşey oluyor:
<img src="/images/javaswing/javaswing3/1.png" />

Genellikle etiketler başka bir elemanı açıklamak için kullanılır.Onuda şöyle yapabilirsiniz:
{%highlight java%}
	etiket.setLabelFor(herhangiBirSwingElemanı);
{%endhighlight%}

### JCheckBox
Açma kapama düğmesi gibi, yada boolean gibi düşünebilirsiniz.Tik atma kutucukları kısacası.Kullanımlarıda çok kolay.CheckBox ları aynı buton kullanır gibi kullanabiliriz.

{%highlight java%}
// chckBox bir class variable olarak tanımlı
chckBox = new JCheckBox("foo"); // "foo" adlı bir checkbox ekledik
chckBox.setBounds(75, 87, 129, 23);
chckBox.addItemListener(this); // Bu sefer ItemListener interfacesinden 
{%endhighlight%}

Classımızın ["ItemListener Interface"](https://docs.oracle.com/javase/7/docs/api/java/awt/event/ItemListener.html) sini ["implement"](http://selimkaratas.com.tr/wp/javada-interface.html) etmeli.

Oluşturulan method da ise chckBox umuzun seçili olup olmadığınız kontrol edebiliriz:

{%highlight java%}
@Override
public void itemStateChanged(ItemEvent arg0) {
	Object kaynak = arg0.getItemSelectable();
	if(kaynak == chckBox) {
	// istediğinizi burda yapınız
	// mesela chckBox işaretlimi değilmi bakabiliriz:
	System.out.println(chckBox.isSelected());
		if(chckBox.isSelected()){
		// eğer işaretliyse, istediğinizi burda yapın
		}
		else{
		// eğer işaretli değilse, istediğinizi burda yapın
		}
	}
}
{%endhighlight%}
Ve sonuçumuz:
<img src="/images/javaswing/javaswing3/2.gif" />

### JComboBox

JComboBox bize seçmemiz için birden fazla seçenek sunuyor.Şöyle ki:
{%highlight java%}
String[] diller = {"Türkçe","İngilizce","Fransızca","Almanca","Rusça"};
JComboBox cmbBox = new JComboBox(diller); // yukarıda ki dillerin olduğu bir combobox yaptık
cmbBox.setBounds(75, 87, 129, 23);
frame.getContentPane().add(cmbBox);
{%endhighlight%}
<img src="/images/javaswing/javaswing3/3.png" />

ActionListener ["implementleyip"](http://selimkaratas.com.tr/wp/javada-interface.html) cmbBox daki hangi elemanı seçtiğimizi alabiliriz.Şöyle ki:

{%highlight java%}
cmbBox.addActionListener(new ActionListener() {
	@Override
	public void actionPerformed(ActionEvent arg0) {
		System.out.println(cmbBox.getSelectedItem());
	}
});
{%endhighlight%}
Ve sonucumuz:
<img src="/images/javaswing/javaswing3/4.gif" />

### JTextArea,JFormattedTextField,JPasswordField
Bunları anlatmaya nerdeyse hiç gerek yok, kısaca 2 cümleyle geçeceğim.

#### JTextArea
JTextFieldin büyütülmüş hali gibi düşünebilirsiniz.

#### JFormattedTextField
JTextFieldden tek farkı bu:
[Stackoverflow da sorulmuş bir soru](https://stackoverflow.com/questions/21190260/jformattedtextfield-instead-of-jtextfield)

#### JPasswordField
Şifre girme işlemi gibi işlemlerde yardımcı oluyor.Girdiğiniz herşey * dönüşüyor.

#### Hepsini kullanalım
JComboBox la birleştirelim yukardaki 3 şeyi.JComboBox da seçilen şeyleri göstersinler.
{%highlight java%}
txtrTrke = new JTextArea();
txtrTrke.setText("Türkçe");
txtrTrke.setBounds(75, 162, 175, 53);
frame.getContentPane().add(txtrTrke);
frame.getContentPane().add(cmbBox);

passwordField = new JPasswordField();
passwordField.setBounds(75, 243, 175, 19);
frame.getContentPane().add(passwordField);

formattedTextField = new JFormattedTextField();
formattedTextField.setBounds(75, 138, 169, 19);
frame.getContentPane().add(formattedTextField);
{%endhighlight%}

Hepsini ekledim

{%highlight java%}
private void initialize() {
	frame = new JFrame();
	frame.setBounds(100, 100, 450, 300);
	frame.getContentPane().setLayout(null);

	String[] diller = {"Türkçe","İngilizce","Fransızca","Almanca","Rusça"};
	JComboBox cmbBox = new JComboBox(diller); // yukarıda ki dillerin olduğu bir combobox yaptık
	cmbBox.setBounds(75, 87, 129, 23);
	cmbBox.addActionListener(new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent arg0) {
			System.out.println(cmbBox.getSelectedItem());
		}
	});

	txtrTrke = new JTextArea();
	txtrTrke.setText("Türkçe");
	txtrTrke.setBounds(75, 162, 175, 53);
	frame.getContentPane().add(txtrTrke);
	frame.getContentPane().add(cmbBox);

	passwordField = new JPasswordField();
	passwordField.setBounds(75, 243, 175, 19);
	frame.getContentPane().add(passwordField);

	formattedTextField = new JFormattedTextField();
	formattedTextField.setBounds(75, 138, 169, 19);
	frame.getContentPane().add(formattedTextField);
}
{%endhighlight%}

initialize methodumuz bu oldu.

Şimdi actionListenerimizi amacımıza göre yoğuralım.
{%highlight java%}
cmbBox.addActionListener(new ActionListener() {
	@Override
	public void actionPerformed(ActionEvent arg0) {
		txtrTrke.setText((String) cmbBox.getSelectedItem());
		passwordField.setText((String) cmbBox.getSelectedItem());
		formattedTextField.setText((String) cmbBox.getSelectedItem());
	}
}); 
{%endhighlight%}
Gördüğünüz gibi tamamdır.Ve sonucumuz:
<img src="/images/javaswing/javaswing3/5.gif" />
