
# OSI KATMANLARI

---

## OSI Nedir ? 
OSI bilgisayarların ağlar aracılığı ile kurmuş olduğu iletişimi denetleyen bir protokoldür.


<html > &#128511 </html>

## OSI Önemi : 

- Ağa bağlı sistem mimarilerini düzenlemek ve modellemek için kullanılabilir.
- Daha hızlı araştırma ve  ve geliştirme imkanı sunar.
- Ağ iletişimi , geliştirmeyi standartlaştırarak sistem hakkında önce bilgi sahibi olmadan oldukça karmaşık sistemleri hızlı anlama , oluşturma ve parçalara ayırma olanağı sağlar.

---
## OSI Modeli : 

1. Physical Layer --> Devices , sensors , controllers
2. Data Link Layer --> Communications , protocols , networks , WiFi
3. Network Layer --> Cloud Infrastructure (public , private , hybrid , managed)
4. Transport Layer --> Big Data , Harvest , Data Ingestion
5. Session Layer --> Data Analytics ; Reporting , Mining , Machine Learning
6. Presantation Layer  --> Applications ; Buildings custom apps with "Thing" Data
7. Application Layer --> People & Process ; Transformational decision making based on "Thing" Apps & Data


### Fiziksel Katman (Physical Layer)  
Fiziksel iletişim ortamını ve bu ortam üzerinden veri iletmek için kullanılır. Veri iletişimi temel olarak dijital ve elektronik sinyallerin fiber optik kablolar , bakır kablolar ve hava gibi çeşitli fiziksel kanallar aracılığıyla aktarılmasıdır.

### Veri Bağ Katmanı ( Data Link Layer) 
Fiziksel katmanın mevcut olduğu bir ağ üzerinden iki makineyi birbirine bağlamak için kullanılan teknolojileri ifade eder. 
Bu katman , veri paketleri halinde kapsüllenmiş dijital sinyaller olan veri çerçevelerini yönetir.

Genelde iki alt katmana ayrılır;
 - [[#^ee058b | MAC (Media Access Control)]]
 - [[#^ba0be2 |LLC (Logic Control Layer)]]


### Ağ Katmanı (Network Layer)  
Ağlarda , iletme ve adresleme gibi kavramlarla ilgilidir. İnternet genelinde IPv4 ve IPv6 ana ağ katmanı protokolleri kullanılır.

### Aktarım Katmanı (Transport Layer)  
Veri paketlerinin kayıp ve hata olmaksızın doğru sırada ulaşmasını ve gerektiğinde sorunsuz bir şekilde kurtarılabilmesini sağlar. 

Bu katmanda yaygın olarak 2 protokol kullanılır;
 - Kayıpsız ve bağlantı tabanlı  __TCP__
 - Kayıplı ve bağlantı bulunmayan __UDP__

### Oturum Katmanı (Session Layer) 
Bir oturumda iki ayrı uygulama arasındaki ağ koordinasyonundan sorumludur. Senkronizasyon çakışmalarını yönetir.
Ağ Dosya Sistemi (NFS)  ve Sunucu İleti Bloğu (SMB) oturum katmanında yaygın olarak kullanılır.

### Sunum Katmanı (Presantation Layer) 
HTML , JSON , CSV sunum katmanındaki verilerin yapısını tanımlar. Uygulamanın gönderip tüketeceği söz dizimini içerir.


### Uygulama Katmanı (Application Layer) 
Kullanıcı verileri ile doğrudan iletişim kurar. HTTP ve SMTP içerir. 


---

# TCP / IP Protokolü

TCP / IP ' de yollanan veriler katmanlara göre paketlenerek yollanır ve alıcıda bu paketler teker teker açılıp veri ulaştırılır. 

TCP / IP ' de 4 katman bulunur;
- Network Interface
- Internet
- Transport
- Application

---

# Network Interface
Verinin kablo üzerinde olacağı yapıyı tanımlayarak 1 ve 0 ların fiziksel olarak görüntülenmesi sağlanır. Ethernet en yaygın kablolu yerel ağ teknolojisidir. 

Ethernet 3 alt katmana sahiptir.

- Logic Control Layer (LLC)
	İnternet katmanındaki frame' in hangi protokol ile geldiğini belirleyerek iletimin MAC ' e geçişini sağlar.
 ^ba0be2
- Media Access Control (MAC)
	Hedef ve kaynak MAC adresleri eklenir. ^ee058b

*LLC ve MAC veri bloğuna kendi başlıklarını ekleyerek tam "frame " yapısını oluştururlar.*

- Physical LAyer
	Tam frame ' i elektrik sinyaline ya da elektromanyetik dalgalara dönüştürür.


![[Pasted image 20260210153134.png | Resim 1]]


--- 

# HTTP Nedir?
Ağa bağlı cihazlar arasında bilgi aktarmak için tasarlanmış bir uygulama katmanı protokolüdür. Ağ protokol yığınının diğer katmanlarının üzerinde çalışır.

## HTTP İçeriği 

- HTTP sürüm türü
- URL
- HTTP yöntemi
- HTTP istek başlıkları
- (Opsiyonel) HTTP gövdesi

## HTTP Metod

En yaygın kullanılan metodlar;

- __GET__
- __POST___

## HTTP İstek Başlıkları
Anahtar - Değer çiftleri halinde saklanan metin bilgilerini içerir

```http
Request Headers
:authority: www.google.com
:method: GET
:path: /
:scheme: https
accept: text/html
accept-encoding: gzip,deflate,br
accept-language: en-US,en; q=0.9
upgrade-insecure-requests: 1
user-agent: Mozilla | 5.0
```

```http
Responsa Headers
cache-control: private,max-age=0
content-encoding: br
content-type: text/html
charset: UTF-8
date: Thu,10 Feb 2026
status: 200
strict-transport-security: max-age=86400
x-frame-options: SAMEORIGIN
```

## HTTP durum kodu nedir?

1. 1 X X  --> Bilgilendirme
2. 2 X X --> Başarı
3. 3 X X --> Yönlendirme 
4. 4 X X --> İstemci Hatası
5. 5 X X --> Sunucu Hatası



