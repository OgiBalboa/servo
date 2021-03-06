# SIKAR HA! GELİŞTİRİCİ GÜNLÜKLERİ
* ## Güncel Versiyon : v0.2
Bu proje Servo motorlar ile hareket ettirilen bir robotun farklı metodlarla kontrol edilmesi üzerine yapılmış bir "Robot Kontrol Ünitesi'dir". Amacımız robotun kontrol yöntemlerini araştırmak ve bu konuda çalışma yapmak isteyen insanlara kaynak oluşturmaktır.

# Yayınlanmış Sürümler
* ### [Sürüm : v0.0.1 -Servo Döndürmek-](#v0.0.1)
* ### [Sürüm : v0.0.2 -SIKAR-HA Kontrol Panel adıyla GUI Yazdık-](#v0.0.2)
  * [Sürüm : v0.0.3 -GUI Güncelleme-](#v0.0.3)
  * [Sürüm : v0.0.4 -GUI Güncelleme-](#v0.0.4)

* ### [Sürüm : v0.1.0 -Arduino ile Seri Haberleşme Denemeleri-](#v0.1.0)
  * [Sürüm : v0.1.1 -Arduino Raspberry Pi ile Haberleşme ( BAŞARILI)-](#v0.1.1)

* #### [Sürüm : v0.1.2 -Serial Kayıt GUI-](#v0.1.2)
  * [Sürüm : v0.1.3 -Serial Kayıt GUI Güncelleme-](#v0.1.3)
* ### [Sürüm : v0.2 -Control Panel v0.2](#v0.2)

# Ek Paketler
* ### [Joystick ile Kontrol](#joystick)

* ### [EMG Sinyalleri ile Kontrol](#myo)

# Yakında
* Motor kontrollerini ve ek işlemleri yalnızca raspberry üzerinden yapmak( threading modülü kullanıp birden fazla loop açarak).(Yakın zamanda)
* Ultrasonik sensör ile robota ek özellikler eklemek. ( Parça bulma, bir engele çarpmama vs.) (Yakın zamanda)
* SIKAR-HA adına özgün bir robot mekanik tasarımı geliştirmek.( Orta vadede)
* Bu yazılımı büyük çaplı robotlar üzerinde kullanmak. ( Uzun vadede)
## v0.0.1 26 Şubat 2019 | Servo Döndürmek <a name="v0.0.1"></a>
Servoya açı parametresi verilip kaydedilir ve servonun "0" pozisyonundan kayıtlı pozisyona döngüde olması sağlanır.

## Nasıl Yapılır Videosu :

* [![Servo döndürmek](http://img.youtube.com/vi/ZuVTEtgH9Ns/0.jpg)](http://www.youtube.com/watch?v=ZuVTEtgH9Ns)

## Update v0.0.2 28 Şubat 2019 | SIKAR-HA Kontrol Panel adıyla GUI Yazmaya Başladık <a name="v0.0.2"></a>
"SIKAR HA!" için GUI yazmaya başladık. İlk hali ControlPanelv1 dosyasındadır. Açıklamaları GUI adlı branch'dan bulabilirsiniz.

* ![GUI-main](https://github.com/marmara-technology/SIKAR-HA/blob/master/ScreenShots/mainmenu.png)
## Update v0.0.3 4 Mart 2019 | GUI Güncelleme <a name="v0.0.3"></a>
GUI temel fonksiyonları yerine getirmek üzere kodlandı. "ControlPanelv1.2". 
İlerlemeye devam etmeden önce robotun mekanik kısmına çalışmak gerekiyor. Mekanik kısım tamamlandıktan sonra yeni bir güncelleme ile görüşmek üzere.
* ![GUI-guncel](https://github.com/marmara-technology/SIKAR-HA/blob/master/ScreenShots/kayit.png)
## Update v0.0.4 10 Mart 2019 | GUI Güncelleme <a name="v0.0.4"></a>
Robotun mekanik parçaları geldi. GUI'de şu değişiklikler yapıldı : 
Menu toolbar eklendi.
Mainmenu düzenlendi, github sayfa linki koyuldu.
Slider ile konum bilgisi gönderme penceresi eklendi.
Diğer menü fonksiyonları için taslaklar oluşturuldu.
ControlPanel v1.2 Python kodları
* ![GUI-yeni](https://github.com/marmara-technology/SIKAR-HA/blob/master/ScreenShots/kayitv1.2.png)
## Update v0.1.0 26 Mart 2019 | Arduino ile Seri Haberleşme <a name="v0.1.0"></a>
Yeni sürüm ! Daha öncelerde robotu RasPi kullanarak hareket ettirdik. Şimdi ise Arduino'yu bir motor sürücü gibi kullanarak robotumuzu kontrol edeceğiz. Bu yeni kontrol programında öncelikle Arduino'yu potla robotu kontrol etmek üzere kodluyoruz. Bu kodlar repodaki " Arduino Motor Sürme " adlı dosyada bulunmakta. Arduino kodları basit bir pot ile servo kontrol etme kodlarıdır. Ancak bundan farklı olarak Serial heaberleşme ile RasPi ye motorların konum bilgilerini gönderiyoruz.
* ![serial](https://github.com/marmara-technology/SIKAR-HA/blob/master/ScreenShots/serial%20kayit.png)

Bunun için şöyle bir algoritma gerçekleştirdik :
Arduino kayıt butonuna basıldığında 4 motordan 4 farklı bilgiyi Raspi ye gönderecek.
Raspi ise bu 4 bilgiyi motorlar için oluşturduğumuz register değişkenlerine aktaracak. Bunu gerçekleştirmek için iki kontrolcü arasında senkronizasyonu doğru sağlamış olmamız gerekiyor. Yazdığımız kodda senkronizasyon sağlamak için Raspi ye counter değeri yazdık. Bu sayıcı arduinodan gelen bilgi sayısını kontrol edecek böylece gelen bilgiler sırayla ve birbirine karışmadan registerlara aktarılacak:
Arduino ---> Motorun açı değerini gönder ve 100 ms bekle.
RasPi ---> Alınan bilgiyi registera yaz ve sayıcıyı 1 arttır ve 100 ms bekle.
## Joystick Ek Paket 27 Nisan 2019 <a name="joystick"></a>
Bu zamana kadar robotu potansiyometre ile kontrol etmiştik. Artık robotu daha kolay kontrol etmek ve daha ince hareketleri gerçekleştirmek üzere Joystick kullanacağız ! Robotu joystick ile kontrol etmek için hala Arduino'yu bir motor sürücü olarak kullanıyoruz. Bununla beraber motorların pozisyonlarını da serial port aracılığıyla Raspberry Pi üzerine aktarıyoruz. Sonraki güncelleme de bu pozisyonları işlemek üzere kullanacağız. !

## Raspberry ve Arduino Haberleşmesi tamamlandı !! 28 Nisan 2019 <a name="v0.1.1"></a>
Robotun konumunu Arduino üzerinden Raspberry Pi'ye aktarmayı başarmıştık. Ancak Raspberry üzerinde kayıtlı olan konumları Arduino'ya aktarıp robotu hareket ettirmek konusunda zorluklar yaşadık. Neyseki bu sorunu halledildi ve yeni sürüm karşınızda !

[Joystick ile Robot Kontrolü ve Hareket Ezberleme - Arduino Kodları](https://github.com/marmara-technology/SIKAR-HA/blob/master/SIKAR-HA%20Control%20Panel/Arduino/Arduino.ino)

## Serial Haberleşme ile Konum Kaydetme GUI Güncellemesi 2 Mayıs 2019 <a name="v0.1.2"></a>
Seri Haberleşme konusunu hallettikten sonra sıra bunu GUI'de programlamaya geldi. GUI üzerinde kaydedilen konumları aktif olarak gösteren Label'lar eklendi. Ve kaydedilen konumu silme özelliği eklendi. Raspberry'ye Arduino'dan gelen konum bilgileri register adındaki listeye yazılmakta. Her veri girşi yapıldığında aynı zamanda Label olarak bir str verisine de kaydediliyor. Böylece konum bilgilerini bilgisayar topluca alıyor ancak kullanıcı ayrı ayrı görüyor ve görsel olarak konumları görebiliyor. Buna ek olarak daha önce yazdığımız programlarda Serial haberleşme aktif olması için Arduino'ya bağlı bir buton kullanıyorduk. Ancak bundan sonra Seriali aktif ettiğimizde Raspi 3. pini Logic 1 konumuna getirecek ve böylece Arduino Raspberry'nin emri ile çalışacak.

* ![konmukayit](https://github.com/marmara-technology/SIKAR-HA/blob/master/ScreenShots/Konumkayit.png)
## Serial Kayit tamamlandı ve Control Panel'e eklendi ! 7 Mayıs 2019 <a name="v0.1.3"></a>
Serial Kayit yapma otomatikleşti ve butonlar tamamen kalktı.
Kayitli pozisyonları bir dizine kaydetme özelliği eklendi.
Kayit dosyasını import etme ve bu dosyayı çalıştırma özelliği eklendi.
Güncel dosya : [Serial Konum Kayit](https://github.com/marmara-technology/SIKAR-HA/tree/master/SIKAR-HA%20Control%20Panel)
[Hareket Ezberleyici Modül Youtube Videosu](https://youtu.be/7Wulxo9lwis)
## Control Panel Güncelleme ! 14 Mayıs 2019 <a name="v0.2"></a>
Program artık birden çok python dosyasına ayrıldı. Bu sayede kod karmaşıklığı ortadan kalktı ve kontrol metodları ayrı ayrı dosylarda saklandı.

SIKARHA-Control Panel adlı dosyada bulunan Programlar klasöründe kontrol yöntemleri bulunmakta.
Kayıtlar isimli dosya ise kullanıcının kendi oluşturduğu programı kaydetmesini sağlıyor. Ve program yeniden açıldığında burdan kayıt dosyasını açabiliyor.
* [ Kotrol Panel Ana dosyası](https://github.com/marmara-technology/SIKAR-HA/blob/master/SIKAR-HA%20Control%20Panel/SIKARHA.py)

* ![Controlpanel](https://github.com/marmara-technology/SIKAR-HA/blob/master/ScreenShots/controlpanel.png)
### Control Panel ile Konum Kaydetmek - Video -
* [![Control Panel](http://img.youtube.com/vi/TrD485RXhUU/0.jpg)](https://www.youtube.com/watch?v=TrD485RXhUU)

## Serial Bağlantı ile ilgili Problem Giderildi 22 Mayıs 2019 <a name="v0.1.3"></a>
Raspberry'nin serial portuna bağladığımız Arduino kablosunun adresi genellikle /dev/ttyACM0 , ACM1 veya ACM2 olmaktadır. Bu kablo her çıkarıldığında adres değişmektedir. Raspberry üzerinde seriali tanımlarken port bilgisini normalde şu şekilde gireriz :
```python
import serial
ser= serial.Serial('/dev/ttyACM0',9600)
```
Ancak port değiştiğinde doğal olarak bu satır hata verecektir ve program çalışmayacaktır. Bu sorunu çözmek için her defasında serial portu kontrol edip python'da değiştirmek yerine şöyle bir çözüm geliştirdik :
```python
while True :
    try:
        deneme = 0
        if deneme ==0:
            try:
              ser= serial.Serial('/dev/ttyACM0',9600)
              break
            except:
                deneme = 1
        if deneme == 1:
            try:
                ser = serial.Serial('/dev/ttyACM1',9600)
                break
            except:
                deneme = 2
        if deneme == 2:
            try:
                ser=serial.Serial('/dev/ttyACM2',9600)
                break
            except:
                 print("HATA ! Lütfen Arduino serial kablosunu kontrol ediniz")
                 break
    except:
        print("BAŞARISIZ")
```         

Bu yöntem sayesinde, portu bulana dek tüm olasılıkları deneyerek programı çalıştıracaktır.
## Myo Armband ile koldaki EMG (Kas) sinyallerinin işlenmesi ve Robot Kontrolü 29 Mayıs 2019 <a name="myo"></a>
* Myo Armband içerisinde emg ve IMU sensörleri bulunan kompakt bir yapıdır. Kendine ait yazılımı ile veya python üzerinde hazırlanmış kodları sayesinde bu sinyalleri işleyip kullanmak mümkün. 
Kodların sahibi ben olmadığımdan dolayı burada paylaşamayacağım. 
Ancak ileride IMU kullanarak özgün bir sistem tasarlanabilir . 
* [![Servo döndürmek](http://img.youtube.com/vi/xaBf3gU4Qsw/0.jpg)](https://www.youtube.com/watch?v=xaBf3gU4Qsw)
