---
published: false
title: İlk Adam Akıllı Program(Java - Swing)
---
> Bu kadar Java swing den sonra ilk adam akıllı programımızı yapmamızın vakti geldi.

Öncelikle ne yapcaz onu bir düşünelim.Bütün programlamacılar hayatında en az bir kere hava durumu ile ilgili bir program yapmıştır, bende öyle birşey yapayım bari.

Bize hava durumunu veren bir [API](http://e-bergi.com/y/api-nedir) lazım.Aslında ondan önce projenin taslağı falan lazım, ama ne aklıma gelirse öyle yapmayı planlıyorum.Neyse, benim önceden kullandığım bir hava durumu API'ı olan [apixu](https://www.apixu.com/)'yu kullanacağım.Siteye girip API keyimizi almamız lazım. Girip signupa basarsanız zaten API keyiniz karşınıza gelecektir.

API keylerimizi paylaşmamamız gerekiyor aslında, ama yenisini alacağım için şuanki API keyimi kodlarda göstereceğim, hepimiz için farklı API keyleri olacağı için, siz benim API keyim yerine kendinizinkini yazın.

{%highlight java%}
private final String API_KEY = "211e950e45f449fe961161110172509";
{%endhighlight%}

Apixu bize bir json dosyası veriyor.Hatırlarsınız [python ile currency exchanger](https://sergenp.github.io/python/2017/04/06/pytonilejson/) yaparken bahsetmiştim.
O yüzden bize json parse sağlayabilecek bir java library lazım.
[Gson Library](http://central.maven.org/maven2/com/google/code/gson/gson/2.3.1/gson-2.3.1.jar) tam da bu işe yarıyor.
Google nin kendi yaptığı bir library.İndirip ekleyelim ve geçelim javamıza.

### _Programımız_

#### Layout

Bu gönderide GridBagLayout kullanacağım. Bu layouta bir "table" a yerleştirir gibi element yerleştirebiliyorsunuz.Hem de JFramemizin boyutunu değiştirdiğimizde güzel bir şekilde elementlerimizin yerini ona göre ayarlıyor.GridBagLayout u anlatmakla zaman harcamak istemiyorum, isterseniz aşağıdaki kodu kopyalayıp "Design" kısmında açıp 3 5 elementi koymaya çalışıp, nasıl çalıştığını anlayabilirsiniz.

{%highlight java%}
package main;

public class Main{
    private JFrame frame;
    private final String API_KEY = "211e950e45f449fe961161110172509";
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
        frame.setBounds(400, 200, 500, 250);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        GridBagLayout gridBagLayout = new GridBagLayout();
        gridBagLayout.columnWidths = new int[] {0};
        gridBagLayout.rowHeights = new int[] {0, 0};
        gridBagLayout.columnWeights = new double[]{1.0};
        gridBagLayout.rowWeights = new double[]{0.0, 1.0};
        frame.getContentPane().setLayout(gridBagLayout);
    }
{%endhighlight%}

Klasik başlangıcımızı yaptık gördüğünüz üzere. Öncelikle söylemem gereken birşey var, burada GUI ın güzelliğiyle ilgilenmiyeceğim, sadece işlevi önemli benim açımdan, zaten ilgilenmeyi istesem büyük ihtimal 2 hafta GUI nasıl yapılır kursu falan almam gerekir.

#### Metodlarımız
Neyse, şimdi bizim ihtiyacımız olan şey, json dosyamızı internet üzerinden almak.Onun için özel bir fonksiyon oluşturalım.

{%highlight java%}
private HttpURLConnection getJSON(String site){
    try {
        URL url = new URL(site);
        HttpURLConnection baglanti = (HttpURLConnection)url.openConnection();
        return baglanti;
    }
    catch(IOException e) {
        return null;
    }
}
{%endhighlight%}

Bu kodumuzla herhangi bir websitesi url sinden cevap alıp onu geri yollayabiliriz.Ama biz Json almak ve onu yollamak istiyoruz, burada gson kullanacağız.
{%highlight java%}
private JsonElement getJSON(String site){
    try {
        URL url = new URL(site);
        HttpURLConnection baglanti = (HttpURLConnection)url.openConnection();
        baglanti.setRequestMethod("GET");
        baglanti.connect();
        JsonParser jp = new JsonParser();
        JsonElement root = jp.parse(new InputStreamReader((InputStream) baglanti.getContent()));
        return root;
    }
    catch(IOException e) {
        return null;
    }
}
{%endhighlight%}

Bu şekilde JsonElementimizi alabiliriz. JsonElementimiz şöyle (Paris ilini aldığımızı varsayarsak):
{%highlight json%}
{
    "location": {
        "name": "Paris",
        "region": "Ile-de-France",
        "country": "France",
        "lat": 48.87,
        "lon": 2.33,
        "tz_id": "Europe/Paris",
        "localtime_epoch": 1508400247,
        "localtime": "2017-10-19 10:04"
    },
    "current": {
        "last_updated_epoch": 1508399100,
        "last_updated": "2017-10-19 09:45",
        "temp_c": 14.0,
        "temp_f": 57.2,
        "is_day": 1,
        "condition": {
            "text": "Partly cloudy",
            "icon": "//cdn.apixu.com/weather/64x64/day/116.png",
            "code": 1003
        },
        "wind_mph": 2.5,
        "wind_kph": 4.0,
        "wind_degree": 120,
        "wind_dir": "ESE",
        "pressure_mb": 1009.0,
        "pressure_in": 30.3,
        "precip_mm": 0.0,
        "precip_in": 0.0,
        "humidity": 82,
        "cloud": 75,
        "feelslike_c": 14.6,
        "feelslike_f": 58.2,
        "vis_km": 10.0,
        "vis_miles": 6.0
    }
}
{%endhighlight%}
Bana bu bilgiler içerisinden, "temp\_c", "wind\_kph", "wind\_degree", "humidity", "feelslike\_c" lazım.
Peki bunları nasıl alabiliriz? Yeni bir method oluşturalım.

{%highlight java%}
private void gosterHavaDurumu() throws IOException {
    String sehirismi = txtehirIsminiGirin.getText();
    String siteUrl = "http://api.apixu.com/v1/current.json?key="+API_KEY+"&q="+sehirismi;
    JsonElement kok = getJSON(siteUrl);
}
{%endhighlight%}

Burdaki sehirismi değişkenimiz, GUI a koyacağımız text fieldden aldığımız değişken olacak, gördüğünüz üzere. JsonElement imizi aldık, şimdi üstünde işlemler yapabiliriz.
{%highlight java%}
private void gosterHavaDurumu() throws IOException {
    String sehirismi = txtehirIsminiGirin.getText();
    String siteUrl = "http://api.apixu.com/v1/current.json?key="+API_KEY+"&q="+sehirismi;
    JsonElement kok = getJSON(siteUrl);
    // getJSON() methodu hata verirse null değeri geri gönderiyor, o yüzden bunu kontrol etmemiz lazım
    if(kok != null) { // eğer null bir kök dosyamız yoksa onun üstünde oynayabiliriz.
        JsonObject simdiki_hava = (JsonObject) kok.getAsJsonObject().get("current");
        String derece_c = "Derece:" + simdiki_hava.get("temp_c") + " °C";
    }
}
{%endhighlight%}
"temp_c" mizi almış olduk. Buradaki:
{%highlight java%}
JsonObject simdiki_hava = (JsonObject) kok.getAsJsonObject().get("current");
{%endhighlight%}
Bize bunu veriyor:
{%highlight json%}
"current": {
        "last_updated_epoch": 1508399100,
        "last_updated": "2017-10-19 09:45",
        "temp_c": 14.0,
        "temp_f": 57.2,
        "is_day": 1,
        "condition": {
            "text": "Partly cloudy",
            "icon": "//cdn.apixu.com/weather/64x64/day/116.png",
            "code": 1003
        },
        "wind_mph": 2.5,
        "wind_kph": 4.0,
        "wind_degree": 120,
        "wind_dir": "ESE",
        "pressure_mb": 1009.0,
        "pressure_in": 30.3,
        "precip_mm": 0.0,
        "precip_in": 0.0,
        "humidity": 82,
        "cloud": 75,
        "feelslike_c": 14.6,
        "feelslike_f": 58.2,
        "vis_km": 10.0,
        "vis_miles": 6.0
    }
{%endhighlight%}
Bu ise:
{%highlight java%}
simdiki_hava.get("temp_c");
{%endhighlight%}
"temp_c" deki olan değeri bize veriyor, yani bu json dosyası için 14.0 değerini veriyor.

Böylelikle istediğimiz diğer değerleride alabiliriz.

{%highlight java%}
private void gosterHavaDurumu() throws IOException {
    String sehirismi = txtehirIsminiGirin.getText();
    String siteUrl = "http://api.apixu.com/v1/current.json?key="+API_KEY+"&q="+sehirismi;
    JsonElement kok = getJSON(siteUrl);
    // getJSON() methodu hata verirse null değeri geri gönderiyor, o yüzden bunu kontrol etmemiz lazım
    if(kok != null) { // eğer null bir kök dosyamız yoksa onun üstünde oynayabiliriz.
        JsonObject simdiki_hava = (JsonObject) kok.getAsJsonObject().get("current");
        String derece_c = "Derece:" + simdiki_hava.get("temp_c") + " °C";
        String ruzgar_hizi = "Rüzgar hızı:" + simdiki_hava.get("wind_kph") + "km/h";
        String ruzgar_acisi = "Rüzgar açısı:" + simdiki_hava.get("wind_degree").getAsString();
        String nem = "Nem:" + simdiki_hava.get("humidity").getAsString() + "%";
        String hissedilen = "Hissedilen:" + simdiki_hava.get("feelslike_c").getAsString();
        JsonObject ulke_ismi_obj = (JsonObject) kok.getAsJsonObject().get("location");
        String ulke_ismi = ulke_ismi_obj.get("country").getAsString();
    }
}
{%endhighlight%}
Bu bilgileri alıp, ekrana yeni bir JFrame çıkartmak istiyorum, yani geçelim diğer Classımıza, ve HavaDurumu.java dosyamıza.

HavaDurumu.java:
{%highlight java%}
package main;

import java.awt.GridBagLayout;
import java.awt.GridBagConstraints;
import java.awt.Insets;

import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.JLabel;
import java.awt.Font;
import javax.swing.SwingConstants;

public class HavaDurumu extends JFrame {
    private JTextField sehir_ismi;
    private JTextArea bilgiler;

    public HavaDurumu(String[] bilgi,String sehirIsmi,ImageIcon resim,String ulke_ismi) {

        setBounds(400, 200, 390, 370);
        GridBagLayout gridBagLayout = new GridBagLayout();
        gridBagLayout.columnWidths = new int[]{0, 0};
        gridBagLayout.rowHeights = new int[]{0, 0, 0, 0};
        gridBagLayout.columnWeights = new double[]{1.0, Double.MIN_VALUE};
        gridBagLayout.rowWeights = new double[]{0.0, 0.0, 1.0, Double.MIN_VALUE};
        getContentPane().setLayout(gridBagLayout);

        JLabel image_label = new JLabel(ulke_ismi);
        image_label.setIcon(resim);
        image_label.setFont(new Font("Tahoma", Font.PLAIN, 24));
        GridBagConstraints gbc_image_label = new GridBagConstraints();
        gbc_image_label.insets = new Insets(0, 0, 5, 0);
        gbc_image_label.gridx = 0;
        gbc_image_label.gridy = 0;
        getContentPane().add(image_label, gbc_image_label);

        sehir_ismi = new JTextField();
        sehir_ismi.setHorizontalAlignment(SwingConstants.CENTER);
        sehir_ismi.setFont(new Font("Tahoma", Font.PLAIN, 24));
        sehir_ismi.setText(sehirIsmi);
        sehir_ismi.setEditable(false);
        GridBagConstraints gbc_sehir_ismi = new GridBagConstraints();
        gbc_sehir_ismi.insets = new Insets(0, 0, 5, 0);
        gbc_sehir_ismi.fill = GridBagConstraints.HORIZONTAL;
        gbc_sehir_ismi.gridx = 0;
        gbc_sehir_ismi.gridy = 1;
        getContentPane().add(sehir_ismi, gbc_sehir_ismi);
        sehir_ismi.setColumns(10);

        bilgiler = new JTextArea();
        bilgiler.setFont(new Font("Monospaced", Font.PLAIN, 30));
        for (String i : bilgi) {
            bilgiler.append(i + "\n");
        }
        bilgiler.setEditable(false);
        bilgiler.setEnabled(false);
        GridBagConstraints gbc_bilgiler = new GridBagConstraints();
        gbc_bilgiler.gridx = 0;
        gbc_bilgiler.gridy = 2;
        getContentPane().add(bilgiler, gbc_bilgiler);
    }
}
{%endhighlight%}
Burda açıklamam gereken birşey göremiyorum, zaten design kısmında yaptım birçoğunu.Bu JFrameyi çalıştırdığımızda(constructorda hiçbir bilgi almadığımızı farzederek) şöyle bir görüntü elde ediyoruz:
<img src="/images/javaswing/javaswing5/1.png"/>

Ve gosterHavaDurumu() methodumuzu buna yönelik güncelleyelim:
{%highlight java%}
private void gosterHavaDurumu() throws IOException {
    String sehirismi = txtehirIsminiGirin.getText();
    String siteUrl = "http://api.apixu.com/v1/current.json?key="+API_KEY+"&q="+sehirismi;
    JsonElement kok = getJSON(siteUrl);
    if(kok != null) {
        JsonObject simdiki_hava = (JsonObject) kok.getAsJsonObject().get("current");
        String derece_c = "Derece:" + simdiki_hava.get("temp_c") + " °C";
        String ruzgar_hizi = "Rüzgar hızı:" + simdiki_hava.get("wind_kph") + "km/h";
        String ruzgar_acisi = "Rüzgar açısı:" + simdiki_hava.get("wind_degree").getAsString();
        String nem = "Nem:" + simdiki_hava.get("humidity").getAsString() + "%";
        String hissedilen = "Hissedilen:" + simdiki_hava.get("feelslike_c").getAsString();
        JsonObject ulke_ismi_obj = (JsonObject) kok.getAsJsonObject().get("location");
        String ulke_ismi = ulke_ismi_obj.get("country").getAsString();

        // resmi al
        JsonObject resimJSONobj = simdiki_hava.get("condition").getAsJsonObject();
        String resimurl = resimJSONobj.get("icon").getAsString();
        URL url = new URL("http:" + resimurl);
        Image c = ImageIO.read(url);
        ImageIcon resim = new ImageIcon(c);
        String[] bilgiler = {derece_c, ruzgar_hizi, ruzgar_acisi, nem, hissedilen};
        // havadurumu göster
        HavaDurumu hava = new HavaDurumu(bilgiler,sehirismi,resim,ulke_ismi);
        hava.setVisible(true);
    }
    else {
        JOptionPane.showMessageDialog(null, "Girilen şehir bulunamadı", "HATA", JOptionPane.ERROR_MESSAGE);
        return;
    }
{%endhighlight%}

Burda açıklanması gereken:

{%highlight java%}
    String resimurl = resimJSONobj.get("icon").getAsString();
    URL url = new URL("http:" + resimurl);
    Image c = ImageIO.read(url);
    ImageIcon resim = new ImageIcon(c);
{%endhighlight%}
Bu 4 satır kodumuz bize bir urlyi okuyup ondan bir resim almamızı sağlıyor.Json dosyamızda bir "icon" değeri var, o "icon" değeri Apixu API ımızda bir resime isabet ki o resim de şimdiki havanın nasıl olduğunu gösteren bir resim.

Şimdi butonumuzu yapıp ona gosterHavaDurumu() methodunu uygulamasını söyleyelim(unutmayın bu kodlar initialize()metodumuzun altında olmalı):
{%highlight java%}
JButton havaDurumuAl = new JButton("Hava Durumunu Al");
havaDurumuAl.setFont(new Font("Tahoma", Font.PLAIN, 24));
GridBagConstraints gbc_havaDurumuAl = new GridBagConstraints();
gbc_havaDurumuAl.anchor = GridBagConstraints.SOUTH;
gbc_havaDurumuAl.gridx = 0;
gbc_havaDurumuAl.gridy = 1;
frame.getContentPane().add(havaDurumuAl, gbc_havaDurumuAl);
havaDurumuAl.addActionListener( (e)-> {
    try {
        gosterHavaDurumu();
    } catch (IOException e1) {
        JOptionPane.showMessageDialog(null, "İnternet bağlantınızı kontrol ediniz", "HATA", JOptionPane.ERROR_MESSAGE);
    }
});
{%endhighlight%}

Şimdide şehir ismi girdiğimiz text fieldimizi yapalım:

{%highlight java%}
txtehirIsminiGirin = new JTextField();
txtehirIsminiGirin.setHorizontalAlignment(SwingConstants.CENTER);
txtehirIsminiGirin.setToolTipText("\u015Eehir \u0130smini Girip, Hava durumu al butonuna bas\u0131n\u0131z.");
txtehirIsminiGirin.setFont(new Font("Tahoma", Font.PLAIN, 30));
GridBagConstraints gbc_txtehirIsminiGirin = new GridBagConstraints();
gbc_txtehirIsminiGirin.insets = new Insets(0, 0, 5, 0);
gbc_txtehirIsminiGirin.gridx = 0;
gbc_txtehirIsminiGirin.gridy = 0;
frame.getContentPane().add(txtehirIsminiGirin, gbc_txtehirIsminiGirin);
txtehirIsminiGirin.setColumns(10);
{%endhighlight%}
txtehirIsminiGirin bir instance variable olduğu için tipini belirtmemize gerek yok.(bkz. [instance variable](https://stackoverflow.com/questions/16686488/java-what-is-an-instance-variable))

Ve sonunda önümüze bu kötü görünümlü ama çalışan güzel program karşımıza çıkıyor:
<img src="/images/javaswing/javaswing5/2.gif"/>

#### Son
ve kodlarımız
##### Main.java
{%highlight java%}
package main;

import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JOptionPane;

import com.google.gson.JsonElement;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

import java.awt.GridBagLayout;
import java.awt.Image;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

import javax.imageio.ImageIO;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import java.awt.GridBagConstraints;
import java.awt.Insets;
import javax.swing.JTextField;
import java.awt.Font;
import javax.swing.SwingConstants;

    public class Main{

    private JFrame frame;
    private final String API_KEY = "211e950e45f449fe961161110172509";
    private JTextField txtehirIsminiGirin;

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
        frame.setBounds(400, 200, 500, 250);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        GridBagLayout gridBagLayout = new GridBagLayout();
        gridBagLayout.columnWidths = new int[] {0};
        gridBagLayout.rowHeights = new int[] {0, 0};
        gridBagLayout.columnWeights = new double[]{1.0};
        gridBagLayout.rowWeights = new double[]{0.0, 1.0};
        frame.getContentPane().setLayout(gridBagLayout);

        txtehirIsminiGirin = new JTextField();
        txtehirIsminiGirin.setHorizontalAlignment(SwingConstants.CENTER);
        txtehirIsminiGirin.setToolTipText("\u015Eehir \u0130smini Girip, Hava durumu al butonuna bas\u0131n\u0131z.");
        txtehirIsminiGirin.setFont(new Font("Tahoma", Font.PLAIN, 30));
        GridBagConstraints gbc_txtehirIsminiGirin = new GridBagConstraints();
        gbc_txtehirIsminiGirin.insets = new Insets(0, 0, 5, 0);
        gbc_txtehirIsminiGirin.gridx = 0;
        gbc_txtehirIsminiGirin.gridy = 0;
        frame.getContentPane().add(txtehirIsminiGirin, gbc_txtehirIsminiGirin);
        txtehirIsminiGirin.setColumns(10);

        JButton havaDurumuAl = new JButton("Hava Durumunu Al");
        havaDurumuAl.setFont(new Font("Tahoma", Font.PLAIN, 24));
        GridBagConstraints gbc_havaDurumuAl = new GridBagConstraints();
        gbc_havaDurumuAl.anchor = GridBagConstraints.SOUTH;
        gbc_havaDurumuAl.gridx = 0;
        gbc_havaDurumuAl.gridy = 1;
        frame.getContentPane().add(havaDurumuAl, gbc_havaDurumuAl);
        havaDurumuAl.addActionListener( (e)-> {
            try {
                gosterHavaDurumu();
            } catch (IOException e1) {
                JOptionPane.showMessageDialog(null, "İnternet bağlantınızı kontrol ediniz", "HATA", JOptionPane.ERROR_MESSAGE);
            }
        });
    }

    private JsonElement getJSON(String site){
        try {
            URL url = new URL(site);
            HttpURLConnection baglanti = (HttpURLConnection)url.openConnection();
            baglanti.setRequestMethod("GET");
            baglanti.connect();
            JsonParser jp = new JsonParser();
            JsonElement root = jp.parse(new InputStreamReader((InputStream) baglanti.getContent()));
            return root;
        }
        catch(IOException e) {
            return null;
        }
    }

    private void gosterHavaDurumu() throws IOException {
        String sehirismi = txtehirIsminiGirin.getText();
        String siteUrl = "http://api.apixu.com/v1/current.json?key="+API_KEY+"&q="+sehirismi;
        JsonElement kok = getJSON(siteUrl);
        if(kok != null) {
            JsonObject simdiki_hava = (JsonObject) kok.getAsJsonObject().get("current");
            String derece_c = "Derece:" + simdiki_hava.get("temp_c") + " °C";
            String ruzgar_hizi = "Rüzgar hızı:" + simdiki_hava.get("wind_kph") + "km/h";
            String ruzgar_acisi = "Rüzgar açısı:" + simdiki_hava.get("wind_degree").getAsString();
            String nem = "Nem:" + simdiki_hava.get("humidity").getAsString() + "%";
            String hissedilen = "Hissedilen:" + simdiki_hava.get("feelslike_c").getAsString();
            JsonObject ulke_ismi_obj = (JsonObject) kok.getAsJsonObject().get("location");
            String ulke_ismi = ulke_ismi_obj.get("country").getAsString();

            // resmi al
            JsonObject resimJSONobj = simdiki_hava.get("condition").getAsJsonObject();
            String resimurl = resimJSONobj.get("icon").getAsString();
            URL url = new URL("http:" + resimurl);
            Image c = ImageIO.read(url); 
            ImageIcon resim = new ImageIcon(c);
            String[] bilgiler = {derece_c, ruzgar_hizi, ruzgar_acisi, nem, hissedilen};
            // havadurumu göster
            HavaDurumu hava = new HavaDurumu(bilgiler,sehirismi,resim,ulke_ismi);
            hava.setVisible(true);
        }
        else {
            JOptionPane.showMessageDialog(null, "Girilen şehir bulunamadı", "HATA", JOptionPane.ERROR_MESSAGE);
            return;
        }
    }
}
{%endhighlight%}
##### HavaDurumu.java:
{%highlight java%}
package main;

import java.awt.GridBagLayout;
import java.awt.GridBagConstraints;
import java.awt.Insets;

import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.JLabel;
import java.awt.Font;
import javax.swing.SwingConstants;

public class HavaDurumu extends JFrame {
    private JTextField sehir_ismi;
    private JTextArea bilgiler;

    public HavaDurumu(String[] bilgi,String sehirIsmi,ImageIcon resim,String ulke_ismi) {

        setBounds(400, 200, 390, 370);
        GridBagLayout gridBagLayout = new GridBagLayout();
        gridBagLayout.columnWidths = new int[]{0, 0};
        gridBagLayout.rowHeights = new int[]{0, 0, 0, 0};
        gridBagLayout.columnWeights = new double[]{1.0, Double.MIN_VALUE};
        gridBagLayout.rowWeights = new double[]{0.0, 0.0, 1.0, Double.MIN_VALUE};
        getContentPane().setLayout(gridBagLayout);

        JLabel image_label = new JLabel(ulke_ismi);
        image_label.setIcon(resim);
        image_label.setFont(new Font("Tahoma", Font.PLAIN, 24));
        GridBagConstraints gbc_image_label = new GridBagConstraints();
        gbc_image_label.insets = new Insets(0, 0, 5, 0);
        gbc_image_label.gridx = 0;
        gbc_image_label.gridy = 0;
        getContentPane().add(image_label, gbc_image_label);

        sehir_ismi = new JTextField();
        sehir_ismi.setHorizontalAlignment(SwingConstants.CENTER);
        sehir_ismi.setFont(new Font("Tahoma", Font.PLAIN, 24));
        sehir_ismi.setText(sehirIsmi);
        sehir_ismi.setEditable(false);
        GridBagConstraints gbc_sehir_ismi = new GridBagConstraints();
        gbc_sehir_ismi.insets = new Insets(0, 0, 5, 0);
        gbc_sehir_ismi.fill = GridBagConstraints.HORIZONTAL;
        gbc_sehir_ismi.gridx = 0;
        gbc_sehir_ismi.gridy = 1;
        getContentPane().add(sehir_ismi, gbc_sehir_ismi);
        sehir_ismi.setColumns(10);

        bilgiler = new JTextArea();
        bilgiler.setFont(new Font("Monospaced", Font.PLAIN, 30));
        for (String i : bilgi) {
            bilgiler.append(i + "\n");
        }
        bilgiler.setEditable(false);
        bilgiler.setEnabled(false);
        GridBagConstraints gbc_bilgiler = new GridBagConstraints();
        gbc_bilgiler.gridx = 0;
        gbc_bilgiler.gridy = 2;
        getContentPane().add(bilgiler, gbc_bilgiler);
    }
}

{%endhighlight%}