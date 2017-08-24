---
published: true
title: Python ile JSON Parsing ve Currency Exchanger Programı
categories: Python
layout: post
---

Python ile fixer.io dan alacağımız JSON dosyasını yararlı bir programa dönüştüreceğiz.

### JSON Nedir?
JSON (JavaScript Object Notation), bazı bilgileri kolay ve insan gözüne güzel gözüken 
bir şekilde toplayan ve .json uzantısıyla kaydeden bir dosya türü diyebiliriz.Örnek olarak:

{%highlight js%}
{
 "maps":[
         {"id":"blabla","iscategorical":"0"},
         {"id":"blabla","iscategorical":"0"}
        ],
"masks":
         {"id":"valore"},
"om_points":"value",
"parameters":
         {"id":"valore"}
}
{%endhighlight%}
Yada bizim kullancağımız olan:
{%highlight js%}
{
"base":"TRY",
"date":"2017-04-05",
"rates":{
    "AUD":0.35745,
    "BGN":0.49635,
    "BRL":0.83682,
    "CAD":0.36268,
    "CHF":0.27175,
    "CNY":1.8688,
    "CZK":6.8668,
    "DKK":1.887,
    "GBP":0.21701,
    "HKD":2.1053,
    "HRK":1.8927,
    "HUF":78.649,
    "IDR":3610.5,
    "ILS":0.99041,
    "INR":17.585,
    "JPY":30.071,
    "KRW":305.22,
    "MXN":5.0802,
    "MYR":1.2007,
    "NOK":2.3263,
    "NZD":0.38877,
    "PHP":13.585,
    "PLN":1.0739,
    "RON":1.1521,
    "RUB":15.141,
    "SEK":2.4299,
    "SGD":0.37935,
    "THB":9.3544,
    "USD":0.27099,
    "ZAR":3.7136,
    "EUR":0.25378
    }
}

{%endhighlight%}
Gibi.
### Python Kısmı
Şimdi gelelim bu dosyayı alıp pythonda nasıl kullanacağımıza.
{%highlight python%}
import json
from urllib.request import urlopen

jsonData = urlopen("http://api.fixer.io/latest?base=TRY")
jsonData = jsonData.read()
print(jsonData)


{%endhighlight%}
Bir siteden veri alıp okumayı böylelikle yapmış bulunuyoruz.Şimdi bu veriyi alıp düzgün şekle sokmamız, sonrada ordan gelen bilgilerle TL yi başka bir para birimine çevirmemiz gerekiyor.Burda python'a ait dictionary kullanabiliriz, fakat ben list leri çok sevdiğim için, list kullanmayı planlıyorum. 

NOT: fixer.io sitesi günlük olarak güncelleniyor, o yüzden aldığımız JSON dosyası bugüne ait, yani herzaman güncel olacak. [fixer.io](http://fixer.io) ya giderek API'nın size sağladığı özellikleri görebilirsiniz.


Pythonun OOP yönünü kullanarak geliştireceğim, böylelikle daha kullanışlı birşey elde edebiliriz.Yukaridaki kodumuz otomatikmen : 
{%highlight python%}
import json
from urllib.request import urlopen

class CurrencyConverter:
	def __init__(self,Currency):
		self.url = urlopen("http://api.fixer.io/latest?base={}".format(Currency))
		self.jsonData = self.url.read()
		print(self.jsonData)

cConverter = CurrencyConverter("TRY")
{%endhighlight%}

Buna dönüşmüş oldu.Burda her yeni class oluşturuşumuzda para biriminin 3 haneli şeklini girip, o birime ait JSON dosyasını alabiliriz.
{%highlight python%}
cConverter = CurrencyConverter("TRY")
cConverter2 = CurrencyConverter("GBP")
cConverter3 = CurrencyConverter("RUB")
{%endhighlight%}
gibi.

Python bir HTML den gelen bilgiyi "byte" olarak okuyor.Bunun üstünde işlem yapmamız için alıp "string" e dönüştürmemiz lazım.Burdada işin içine json library ve decode miz giriyor:

{%highlight python%}
import json
from urllib.request import urlopen

class CurrencyConverter:
	def __init__(self,Currency):
    		self.baseCurrency = Currency
        	self.url = urlopen("http://api.fixer.io/latest?base={}".format(Currency))
        	self.jsonData = json.loads(self.url.read().decode("utf-8"))

cConverter = CurrencyConverter("TRY")
{%endhighlight%}
[Buradan bu sorunla ilgili bir stackoverflow sorusuna bakabilirsiniz.](http://stackoverflow.com/questions/6862770/python-3-let-json-object-accept-bytes-or-let-urlopen-output-strings)
Böylelikle JSON dosyamızı güzel bir şekilde kullanabiliriz.Şimdi class ımızı alıp daha ileri götürmemiz lazım, İlk para birimimiz ve dönüştürmemiz gereken para birimini ekleyerek yapabiliriz:
{%highlight python%}
import json
from urllib.request import urlopen

class CurrencyConverter:
	def __init__(self,Currency,toCurrency):
    		self.baseCurrency = Currency
        	self.toCurrency = toCurrency
        	self.url = urlopen("http://api.fixer.io/latest?base={}".format(self.baseCurrency))
        	self.jsonData = json.loads(self.url.read().decode("utf-8"))
            
           
           
cConverter = CurrencyConverter("TRY","USD")
{%endhighlight%}

Geldik şimdi JSON dosyamızdan gereken bilgiyi nasıl almamız gerektiğine.

JSON dosyamızda gördüğümüz üzere bizim istediğimiz bilgi "rates" adı altında, peki buna nasıl erişiriz?
{%highlight python%}
self.jsonData["rates"][self.toCurrency]
{%endhighlight%}
İle istediğimiz çarpana erişmiş oluruz.Geriye kalan sadece girmeniz gereken sayı.

{%highlight python%}
import json
from urllib.request import urlopen

class CurrencyConverter:
	def __init__(self,Currency,toCurrency):
    		self.baseCurrency = Currency
        	self.toCurrency = toCurrency
        	self.url = urlopen("http://api.fixer.io/latest?base={}".format(self.baseCurrency))
        	self.jsonData = json.loads(self.url.read().decode("utf-8"))

	def calculate(self,Amount):
    		self.Amount = Amount
        	self.convertedCurrency = self.jsonData["rates"][self.toCurrency]*self.Amount
        	print("{} {} is {} {}".format(self.Amount,self.baseCurrency,self.convertedCurrency,self.toCurrency))


cConventer = CurrencyConverter("TRY","EUR")
cConventer.calculate(20)
#20 TRY is 5.0568 EUR 
cConverter2 = CurrencyConverter("EUR","USD")
cConverter2.calculate(50)
#50 EUR is 53.33 USD 
#>>Tabiki bunlar bugünün rakamları 06.04.2017 <<
{%endhighlight%}

Böylelikle programımız tamamlanmış oldu.
