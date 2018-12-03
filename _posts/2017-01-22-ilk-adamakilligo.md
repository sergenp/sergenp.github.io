---
published: true
layout: post
title: İlk Adam Akıllı Program(Go)
categories: Golang
tags: 
- ilkprogram
---
{%highlight go%}
    fmt.Printf("ilk adam akıllı program")
{%endhighlight%}
Geri sayım programı yapayım dedim.Hazır elimin altındada Go var.Problemi düşünmekten başlayalım.

1. [ ] Main fonksiyonu oluştur 
   2. [ ] Kullanıcıdan zaman bilgisi al
   3. [ ] Alınan zaman bilgisi dakika:saniye cinsinden olsun
   4. [ ] Bu bilgileri array a kaydet
   5. [ ] mins,secs değişkenleri oluştur ve arraydakileri bunlara ata
2. [ ] Geri sayım fonksiyonu oluştur
   1. [ ] sonsuz loop oluştur
   2. [ ] Bir saniye bekle sonra,
   3. [ ] Kullanıcıya kalan zamanın bilgisini ver,
   4. [ ] saniye = saniye - 1
   5. [ ] eğer saniye 0 a ulaşırsa saniyeyi 59 yap, dakikayı 1 eksilt
   6. [ ] eğer dakika 0 dan küçük bir değer alırsa, programı sonlandır, looptan çık

Countdown.go olarak adlandırdım dosyamızı.

{%highlight go%}
package main
import "bufio"
import "os"
import "fmt"

func main(){
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Enter time to countdown as this format: 10:20, 5:58 etc.")
	fmt.Printf("Enter Time: ")
	text, _ := reader.ReadString('\n')
}
{%endhighlight%}
1. [X] Main fonksiyonu oluştur 
   2. [X] Kullanıcıdan zaman bilgisi al
   3. [ ] Alınan zaman bilgisi dakika:saniye cinsinden olsun
   4. [ ] Bu bilgileri array a kaydet
   5. [ ] mins,secs değişkenleri oluştur ve arraydakileri bunlara ata
2. [ ] Geri sayım fonksiyonu oluştur
   1. [ ] sonsuz loop oluştur
   2. [ ] Bir saniye bekle sonra,
   3. [ ] Kullanıcıya kalan zamanın bilgisini ver,
   4. [ ] saniye = saniye - 1
   5. [ ] eğer saniye 0 a ulaşırsa saniyeyi 59 yap, dakikayı 1 eksilt
   6. [ ] eğer dakika 0 dan küçük bir değer alırsa, programı sonlandır, looptan çık

 
 İlk iki işimiz bitti.
 
{%highlight go%}
text, _ := reader.ReadString('\n') 
// golang in güzel özelliklerinden biride fonksiyonundan 2 tane output çıkabilmesi
// ReadString methoduda bize 2 tane output veriyor. 
// Biri okunan string tabiki diğeri ise error.
// go da try-catch bulunmadığından böyle birşeye gerek bulunuyor.
// golang bir değişkeni kullanmadığınız takdirde size hata verip programı sonlandırıyor.
// eğer kullanmayacağınız bir değişken tanımlayacaksanız _ kullanmanız gerekmekte.
{%endhighlight%}

{%highlight go%}
package main
import ( 
	// tek tek import "bufio" import "strings" ... yazmaktansa import parantezinde hepsini yazabiliriz.
	// Gonun güzel özelliklerinden birisi
	"bufio"
	"strings"
	"os"
	"strconv"
	"fmt"
)
func main(){
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Enter time to countdown as this format: 10:20, 5:58 etc.")
	fmt.Printf("Enter Time: ")
	text, _ := reader.ReadString('\n')
	timez := strings.Split(text, ":")
	timez[1] = strings.Replace(timez[1],"\r\n","", -1)
	
	/* 

	timez := strings.Split(text, ":") den gelen ikinci değer "30\r\n" gibi bişey oluyor, o yüzden
	golang parseFloat hata veriyor. \r\n leri "" ile değiştirince "30" yapıyoruz, bu yüzden hatasız devam ediyoruz.

	*/ 
	
	mins, err := strconv.Atoi(timez[0]); if (err != nil){panic(err);};
	secs, err := strconv.Atoi(timez[1]); if (err != nil){panic(err);};
	countdown(mins,secs) // şimdide bu fonksiyonumuzu yapmamız gerekiyor.
}

{%endhighlight%}

Main fonksiyonumuzu tamamlamış bulunmaktayız.Gördüğünüz üzere bu sefer ikinci değişkeni kullandım.Çünkü hatayı kullanıcıya bildirmesini istiyorum.

1. [X] Main fonksiyonu oluştur 
   2. [X] Kullanıcıdan zaman bilgisi al
   3. [X] Alınan zaman bilgisi dakika:saniye cinsinden olsun
   4. [X] Bu bilgileri array a kaydet
   5. [X] mins,secs değişkenleri oluştur ve arraydakileri bunlara ata
2. [ ] Geri sayım fonksiyonu oluştur
   1. [ ] sonsuz loop oluştur
   2. [ ] Bir saniye bekle sonra,
   3. [ ] Kullanıcıya kalan zamanın bilgisini ver,
   4. [ ] saniye = saniye - 1
   5. [ ] eğer saniye 0 a ulaşırsa saniyeyi 59 yap, dakikayı 1 eksilt
   6. [ ] eğer dakika 0 dan küçük bir değer alırsa, programı sonlandır, looptan çık

 
 Şimdi geri sayım fonksiyonumuzu oluşturalım.

{%highlight go%}
package main
import (
	"fmt"
	"bufio"
	"strings"
	"os"
	"strconv"
	"time"

)
func main(){
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Enter time to countdown as this format: 10:20, 5:58 etc.")
	fmt.Printf("Enter Time: ")
	text, _ := reader.ReadString('\n')
	timez := strings.Split(text, ":")
	timez[1] = strings.Replace(timez[1],"\r\n","", -1)
	/* 

	timez := strings.Split(text, ":") den gelen ikinci değer "30\r\n" gibi bişey oluyor, o yüzden
	golang parseFloat hata veriyor. \r\n leri "" ile değiştirince "30" yapıyoruz, bu yüzden hatasız devam ediyoruz.

	*/ 
	mins, err := strconv.Atoi(timez[0]); if (err != nil){panic(err);};
	secs, err := strconv.Atoi(timez[1]); if (err != nil){panic(err);};
	countdown(mins,secs) // şimdide bu fonksiyonumuzu yapmamız gerekiyor.
}
func countdown(min,sec int) {
  // go da sadece for yazarsanız while true ile aynı işlevi görüyor.
	for{
    	time.Sleep(time.Second)
        fmt.Printf("%.2v:%.2v\r", min, sec)
        sec = sec - 1
    }
}
{%endhighlight%}
1. [X] Main fonksiyonu oluştur 
   2. [X] Kullanıcıdan zaman bilgisi al
   3. [X] Alınan zaman bilgisi dakika:saniye cinsinden olsun
   4. [X] Bu bilgileri array a kaydet
   5. [X] mins,secs değişkenleri oluştur ve arraydakileri bunlara ata
2. [ ] Geri sayım fonksiyonu oluştur
   1. [X] sonsuz loop oluştur
   2. [X] Bir saniye bekle sonra,
   3. [X] Kullanıcıya kalan zamanın bilgisini ver,
   4. [X] saniye = saniye - 1
   5. [ ] eğer saniye 0 a ulaşırsa saniyeyi 59 yap, dakikayı 1 eksilt
   6. [ ] eğer dakika 0 dan küçük bir değer alırsa, programı sonlandır, looptan çık


{%highlight go%}
package main
import (
	"bufio"
	"fmt"
	"strings"
	"os"
	"time"
	"strconv"

)
func main(){
	reader := bufio.NewReader(os.Stdin)
	fmt.Println("Enter time to countdown as this format: 10:20, 5:58 etc.")
	fmt.Printf("Enter Time: ")
	text, _ := reader.ReadString('\n')
	timez := strings.Split(text, ":")
	timez[1] = strings.Replace(timez[1],"\r\n","", -1)
	/* 

	timez := strings.Split(text, ":") den gelen ikinci değer "30\r\n" gibi bişey oluyor, o yüzden
	golang parseFloat hata veriyor. \r\n leri "" ile değiştirince "30" yapıyoruz, bu yüzden hatasız devam ediyoruz.

	*/ 
	mins, err := strconv.Atoi(timez[0]); if (err != nil){panic(err);};
	secs, err := strconv.Atoi(timez[1]); if (err != nil){panic(err);};
	countdown(mins,secs) // şimdide bu fonksiyonumuzu yapmamız gerekiyor.
}
func countdown(min,sec int) {
// go da sadece for yazarsanız while true ile aynı işlevi görüyor.
	for{  
    	time.Sleep(time.Second)
        fmt.Printf("%.2v:%.2v\r", min, sec)
        sec = sec - 1
        if sec < 0 {
		min -= 1
		sec = 59
		}
        if min < 0 {
		fmt.Println("Countdown finished")
		break
		}
    }
}
{%endhighlight%}
1. [X] Main fonksiyonu oluştur 
   2. [X] Kullanıcıdan zaman bilgisi al
   3. [X] Alınan zaman bilgisi dakika:saniye cinsinden olsun
   4. [X] Bu bilgileri array a kaydet
   5. [X] mins,secs değişkenleri oluştur ve arraydakileri bunlara ata
2. [X] Geri sayım fonksiyonu oluştur
   1. [X] sonsuz loop oluştur
   2. [X] Bir saniye bekle sonra,
   3. [X] Kullanıcıya kalan zamanın bilgisini ver,
   4. [X] saniye = saniye - 1
   5. [X] eğer saniye 0 a ulaşırsa saniyeyi 59 yap, dakikayı 1 eksilt
   6. [X] eğer dakika 0 dan küçük bir değer alırsa, programı sonlandır, looptan çık

 
 Programımız tamamdır! cmd yi açıp go run Countdown.go yazdığınız zaman programı çalıştırabilirsiniz.
