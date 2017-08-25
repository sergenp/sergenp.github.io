---
published: true
layout: post
title: Java Swing(III) - JSwing elemanları
category: Java
tags:
  - swing
---
{%highlight java%}
//JLabel,JComboBox,JCheckBox,JRadioButton,JToggleButton,JTextArea,JFormattedTextField,JPasswordField,
//JTextPane,JEditorPane,JSpinner,JList,JTable,JTree,JProgressBar,JScroolBar,JSeperator,JSlider
{%endhighlight%}
Hah, "Swing components" lerden kalan yukarıda yazanlarıda bu yazıda halledelim.

#### JLabel

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
<img src="/images/javaswing/javaswing2/1.png" />

Genellikle etiketler başka bir elemanı açıklamak için kullanılır.Onuda şöyle yapabilirsiniz:
{%highlight java%}
	etiket.setLabelFor(herhangiBirSwingElemanı);
{%endhighlight%}
