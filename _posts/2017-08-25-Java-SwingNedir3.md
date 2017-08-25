---
published: false
---
{%highlight java%}
//JLabel,JComboBox,JCheckBox,JRadioButton,JToggleButton,JTextArea,JFormattedTextField,JPasswordField,
//JTextPane,JEditorPane,JSpinner,JList,JTable,JTree,JProgressBar,JScroolBar,JSeperator,JSlider
{%endhighlight%}
Hah, "Swing components" lerden kalan yukarıda yazanlarıda bu yazıda halledelim.

Kolaylık açısından bu elemanları gösterirken Absolute Layout kullanacağım.

#### JLabel

Label, adı üstünde etiket, bu güzel kolay kullanımlı elemanımız, etiketlemeye yarıyor.
Etiketi bir resimle, sadece yazıyla veya sadece resimle kullanabilirsiniz.

{%highlight java%}
  ImageIcon resim = createImageIcon("resim/s.gif"); // s.gif diye bir resmimiz olduğunu düşünelim
  etiket1 = new JLabel("Image and Text",
                      icon,
                      JLabel.CENTER);
                      
  //etiketimizi iconumuzun olduğu konuma göre yerini belirliyoruz.
  //resmimiz ve yazımızı bir kare olarak düşünürsek, 
  
  etiket1.setVerticalTextPosition(JLabel.BOTTOM); // dikey olarak karemizin en altına
  etiket1.setHorizontalTextPosition(JLabel.CENTER); // yatay olarak karemizin ortasına
  // konumlandırmış oluyoruz yazımızı
  
  etiket2 = new JLabel("Sadece Yazı"); // sadece yazılı bir etiket
  etiket2 = new JLabel(resim);  // sadece resimli bir etiket
{%endhighlight%}

Genellikle etiketler başka bir elemanı açıklamak için kullanılır.Onuda şöyle yapabilirsiniz:
{%highlight java%}
	etiket.setLabelFor(herhangiBirSwingElemanı);
{%endhighlight%}












