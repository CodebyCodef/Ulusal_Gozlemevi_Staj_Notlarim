

Mesajlaşma sistemleri genel olarak uygulamaların eşzamansız veri alışverişi yapmasını ve birbirinden bağımsız çalışabilmesini sağlar. 

## <span  style="color:purple">ZeroMQ : </span>
-  Aracısız (brokerless) çalışan, temel ağ soketlerine (TCP, IPC) mesajlaşma yetenekleri ekleyen süper hızlı bir kütüphanedir.

## <span style="color:purple">RabbitMQ:</span>
-  Geleneksel ve esnek mesaj yönlendirmesi yapan, AMQP (Advanced Message Queuing Protocol : asenkron mesajlaşma sağlar.) protokolüne dayalı tam teşekküllü bir mesaj aracısıdır. (message broker)

## <span style="color:purple">Kafka:</span>
-  Devasa veri akışlarını (streaming) ve olayları diske kaydederek işlemek için kullanılan dağıtır bir olay akış platformudur.

## <span style="color:purple">MqTT:</span>
-  Özellikle IoT (Nesnelerin İnterneti) cihazları için tasarlanmış, çok düşük bant genişliği tüketen ve kararsız ağlarda bile çalışabilen hafif bir protokoldür.


--- 

### Producer (Üretici): 

- Veriyi (mesajı) oluşturan ve sisteme gönderen uygulamadır.

### Consumer (Tüketici):

- Gönderilenveriyi alıp işleyen, görevini yerine getiren uygulamadır. 

### Message/Event (Mesaj/Olay):

- Üreticiden tüketiciye aktarılan bilginin paketlenmiş halidir.

### Message Broker (Mesaj Aracısı):

- Üretici ve tüketici arasında köprü görevi gören, mesajları teslim alan, gerekirse saklayan e doğru hedefe yönlendiren sunucu yazılımıdır. 

- #### Amaç:
	- Üretici ve tüketici birbirini doğrudan tanımasını (tight coupling) engeller. Böylece biri çökerse diğeri etkilenmez.


### Queue (Kuyruk):

- Mesajların tüketiciye ulaştırılmadan önce bekletildiği veri yapısıdır.

- Genellikle __İlk Giren İlk Çıkar (FIFO)__ mantığıyla çalışır. Mesaj kuyruğa girer, sıradaki tüketici mesajı alır, işler ve işlem bitince mesaj kuyruktan silinir.


### Topic (Konu/Başlık):

- Mesajların belirli bir kategoriye veya etikete göre gruplandırıldığı iletişim kanalıdır.

- Kuyruktan farklı olarak, bir "Topic" e gönderilen mesaj, o konuya ilgi duyan tüm tüketicilere dağıtılır.

--- 

## Mesajlaşma Modelleri (Messaging Patterns)

### 1. Point to Point:

- Bir mesaj yalnızca __tek bir tüketici__ tarafından alınır ve işlenir. 
	
	- __Kullanım Senaryosu__ : Yoğun video işleme görevleri. Bir videoyu birden fazla sunucunun aynı anda işlemesini istemezsin, boştaki ilk sunucunun alp yapması yeterlidir. 

### 2. Publish / Subscribe:

- Üreticinin mesajı yayınladığı, o kanala abone olan __birden fazla__ tüketicinin mesajı aynı anda aldığı modeldir.

	- __Kullanım Senaryosu__ : Bir e-ticaret sitesinde sipariş onaylandığında; "Fatura" servisinin, "Stok" servisinin ve "Kargo" servisinin aynı anda bu olaydan haberdar olup kendi işlemlerini başlatması.

### 3.  Acknowledgement (ACK/NACK):

- Tüketicinin aracıya (broker) verdiği geri bildirimdir. Veri kaybını önlemenin temel taşıdır. 

- __ACK (Acknowledge)__ : "Mesajı aldım ve başarıyla işledim, artık kuyruktan silebilirsin."

- __NACK (Negative Acknowledge)__ "Mesajı işlerken hata oluştu, işleyemedim, lütfen başkasına gönder veya tekrar gönder."

---
---


# <span style="color:rgb(0, 176, 240)">ZeroMQ </span>

ZeroMQ (ØMQ, 0MQ veya zmq olarak da yazılır), adındaki "Zero" (Sıfır) kelimesini **"Sıfır Aracı" (Zero Broker)** olmasından alır. Yani RabbitMQ veya Kafka gibi ayrı bir sunucuya kurup çalıştırdığın devasa bir sistem **değildir**. Uygulamanın içine dahil ettiğin süper akıllı ve hafif bir kütüphanedir.


### ZeroMQ'nun Temel İletişim Modelleri (Patterns)

ZeroMQ, uygulamaların birbiriyle nasıl konuşacağına dair hazır şablonlar sunar. En çok kullanılan 3 tanesi şunlardır:

- **1. REQ - REP (Request - Reply / İstek - Yanıt):**
    
    - Klasik HTTP (Web) mantığına çok benzer. İstemci (Client) bir istek gönderir ve sunucudan (Server) bir yanıt bekler.
        
    - **Senkron** çalışır. Yani REQ gönderen taraf, REP gelene kadar başka işlem yapmaz, bekler.
        
- **2. PUB - SUB (Publish - Subscribe / Yayınla - Abone Ol):**
    
    - Bir üretici (Publisher) mesajı yayınlar, o kanala abone olan tüm tüketiciler (Subscriber) mesajı aynı anda alır.
        
    - Canlı borsa verisi yayınlamak veya anlık hava durumu bildirimleri göndermek için idealdir. (Publisher, abone var mı yok mu ilgilenmez, sadece bağırır).
        
- **3. PUSH - PULL (Pipeline / Boru Hattı):**
    
    - Ağır bir işi, birden fazla işçiye (worker) paylaştırmak için kullanılır.
        
    - **PUSH** eden taraf (Dağıtıcı) işleri hatta bırakır. **PULL** eden taraflar (İşçiler) boşa çıktıkça sıradaki işi alıp işler. Paralel hesaplama (Parallel Computing) için biçilmiş kaftandır.

### Avantajları (Neden Kullanılır?)

- **İnanılmaz Hızlıdır:** Ortada mesajı diske yazıp bekletecek hantal bir aracı (broker) olmadığı için gecikme (latency) mikrosaniyeler seviyesindedir.
    
- **Merkezi Çökme Noktası Yoktur (No Single Point of Failure):** RabbitMQ sunucusu çökerse tüm haberleşme durur. ZeroMQ'da ise düğümler (node) birbiriyle doğrudan konuştuğu için sistemin tamamı tek bir sunucuya bağlı değildir.
    
- **Hafiftir:** Kurulum veya yapılandırma gerektirmez, sadece koda kütüphane olarak eklenir.


---

# <span style="color:rgb(0, 176, 240)"> RabbitMQ </span>


ZeroMQ'da "ortada bir sunucu yok" demiştik. RabbitMQ ise tam tersidir. Ortada **"Broker"** dediğimiz, mesajları teslim alan, güvenle saklayan ve doğru yere teslim eden gerçek bir sunucu/hizmet vardır.

RabbitMQ, **AMQP (Advanced Message Queuing Protocol)** adı verilen çok yetenekli bir standart üzerine kuruludur. En büyük gücü, mesajları hedefine ulaştırırken sunduğu **esnek yönlendirme (routing)** yeteneğidir.

RabbitMQ'nun anatomisini anlamak için bilmen gereken en kritik kavram **Exchange**'dir.

### Exchange (Santral / Yönlendirici)

RabbitMQ'da üretici (Producer) mesajı doğrudan kuyruğa (Queue) **göndermez**. Mesajı önce "Exchange" adı verilen santrale gönderir. Exchange, önceden belirlenmiş kurallara (**Binding**) bakarak mesajın hangi kuyruğa (veya kuyruklara) gideceğine karar verir.

RabbitMQ'da 4 temel Exchange tipi vardır (Burası mülakatlarda çok sorulur, yıldızlayabilirsin):

- **1. <span style="color: rgb(235, 120, 129)"> Direct Exchange (Doğrudan Yönlendirme):</span>
    
    - Mesajın üzerindeki etiket (Routing Key) ile kuyruğun etiketi **birebir** eşleşiyorsa mesaj o kuyruğa gider.
        
    - _Örnek:_ Etiketi "video.render" olan bir mesaj, sadece "video.render" isimli kuyruğa düşer. Nokta atışı gönderimdir.
        
- **2.  <span style="color: rgb(235, 120, 129)"> Fanout Exchange (Yayın / Megafon): </span>
    
    - Mesajın etiketine hiç bakmaz. Gelen mesajı, kendisine bağlı olan **tüm kuyruklara** kopyalayarak gönderir.
        
    - _Örnek:_ Bir e-ticaret sitesinde "Sipariş Tamamlandı" olayı gerçekleştiğinde; Fatura, Stok ve Kargo kuyruklarının hepsine aynı anda bu bilginin gönderilmesi.
        
- **3.  <span style="color: rgb(235, 120, 129)"> Topic Exchange (Konu / Desen Eşleşmesi): </span>
    
    - Direct Exchange'in daha akıllı halidir. Birebir eşleşme yerine __joker karakterler (_ ve #)_* kullanarak desen (pattern) eşleşmesi yapar.
        
    - _Kural:_ `*` (yıldız) tek bir kelimeyi, `#` (kare) ise sıfır veya daha fazla kelimeyi temsil eder.
        
    - _Örnek:_ `log.error.*` etiketli bir kuyruk; `log.error.database` ve `log.error.server` mesajlarını alır ama `log.warning.database` mesajını almaz. Sistem loglarını ayırmak için mükemmeldir.
        
- **4.  <span style="color: rgb(235, 120, 129)"> Headers Exchange: </span>
    
    - Yönlendirmeyi etiket (Routing Key) ile değil, mesajın "Header" (başlık) kısmındaki verilere (Key-Value) göre yapar. Daha karmaşık kurallar için kullanılır ama Topic kadar yaygın değildir.
        

### <span style="color: rgb(130, 212, 127)"> RabbitMQ'nun Avantajları </span>

- **Güvenilirlik (Reliability):** Tüketici çökse bile mesajlar kuyrukta bekler (Hatta diske yazılıp kalıcı hale getirilebilir - Persistence). Tüketici ayağa kalktığında kaldığı yerden devam eder.
    
- **ACK Mekanizması:** Önceki bölümde bahsettiğimiz "Mesajı başarıyla işledim" (ACK) veya "Hata oldu, tekrar kuyruğa al" (NACK) mantığı kusursuz çalışır. Veri kaybı riski çok düşüktür.
    
- **Esneklik:** Exchange tipleri sayesinde çok karmaşık senaryoları kolayca yönetebilirsin.



---

# <span style="color:rgb(0, 176, 240)"> Apache Kafka </span>


Önceki bölümde RabbitMQ'nun mesajı teslim ettikten (ve ACK onayını aldıktan) sonra kuyruktan sildiğini söylemiştik. **Kafka ise mesajı silmez, diske yazar.** Kafka, geleneksel bir "mesaj kuyruğu" olmaktan ziyade, olayların (events) uç uca eklendiği devasa ve dağıtık bir **Log (Kayıt Defteri)** sistemidir. Bu yapısı sayesinde saniyede milyonlarca mesajı yutabilir.

Kafka'yı anlamak için şu üç temel kavrama hakim olmak şarttır:

### 1. <span style="color: rgb(235, 120, 129)">Log Tabanlı Topic (Konu) </span>

Kafka'da da mesajlar Topic'lere gönderilir ama buradaki Topic bir kuyruk değil, **Append-Only (Sadece Sona Ekleme Yapılan)** bir kaset veya seyir defteri gibidir. Yeni gelen mesaj hep en sona eklenir. Geçmişteki mesajlar değiştirilemez.

### 2. <span style="color: rgb(235, 120, 129)">Partition (Bölümleme) </span>

Eğer saniyede milyonlarca veri geliyorsa, tek bir sunucu (veya tek bir dosya) bunu kaldıramaz. Kafka, bir Topic'i parçalara böler. Buna **Partition** denir.

- Her Partition farklı bir sunucuda (Broker) tutulabilir. Bu sayede sistem yatayda sınırsız büyüyebilir (Horizontal Scaling). Kafka'nın devasa verilerle başa çıkabilmesinin sırrı budur.
    

### 3.<span style="color: rgb(235, 120, 129)"> Offset (Konum / İşaretçi) </span>

RabbitMQ'da mesajın okunup okunmadığını Broker (sunucu) takip ediyordu. Kafka'da ise bu sorumluluk **Tüketiciye (Consumer)** aittir.

- Partition içine yazılan her mesaja sıralı bir ID numarası verilir. Buna **Offset** denir.
    
- Tüketici, "Ben şu an 45. Offset'teki mesajı okudum" diye aklında tutar.
    

Diyelim ki anlık olarak akan müşteri demografisi verilerinden ürün kategorisi tahmini yapan bir derin öğrenme modeli çalıştırıyorsun. İstanbul perakende trendleri gibi yoğun bir kaynaktan sisteme saniyede on binlerce işlem verisi (event) aktığında, modelinin bu hıza anında yetişmesi imkansızdır. Kafka, bu devasa veri selini Partition'larına diske yazarak tamponlar. Derin öğrenme modelin (Consumer) çökerse veya yeniden başlatılırsa hiçbir veri kaybolmaz; model ayağa kalktığında kaldığı **Offset'ten (kaldığı satırdan)** okumaya ve tahmin üretmeye tıkır tıkır devam eder.

### <span style="color: rgb(130, 212, 127)">Kafka'nın Avantajları </span>

- **Replayability (Yeniden Oynatabilme):** Veriler diskte belirli bir süre (örneğin 7 gün) tutulduğu için, bir hata yaptığında "Tüketiciyi başa sar, verileri baştan tekrar işle" diyebilirsin.
    
- **Muazzam Performans (Throughput):** Disk okuma/yazma işlemlerini ardışık (sequential) yaptığı için inanılmaz hızlıdır. Big Data (Büyük Veri) ve anlık veri akışı (Streaming) projelerinin kalbidir.



---


# <span style="color: rgb(0, 176, 240)"> MqTT </span>


Önceki sistemler (RabbitMQ, Kafka) genellikle güçlü sunucularda, devasa veri merkezlerinde ve stabil ağ bağlantılarında çalışmak üzere tasarlanmıştır. Ancak işin içine **akıllı saatler, sıcaklık sensörleri, mobil cihazlar veya araç takip sistemleri** girdiğinde işler değişir.

Bu cihazların pili azdır, işlemci güçleri düşüktür ve bağlandıkları ağ (örneğin 3G/Edge veya zayıf bir Wi-Fi) her an kopabilir. İşte MQTT tam olarak bu zorlu koşullar için icat edilmiş **son derece hafif (lightweight)** bir protokoldür.

MQTT de tıpkı diğerleri gibi **Pub/Sub (Yayınla ve Abone Ol)** mantığıyla çalışır ve ortada bir **Broker** (Aracı sunucu, örn: Mosquitto, HiveMQ) bulunur. Ancak onu özel yapan birkaç "hayat kurtarıcı" kavram vardır:

### 1. <span style="color: rgb(235, 120, 129)"> Hiyerarşik Topic (Konu) Yapısı </span>

MQTT'de Topic'ler tıpkı bilgisayarındaki dosya dizinleri gibi `/` (eğik çizgi) ile ayrılır. Bu, milyonlarca cihazı yönetmeyi çok kolaylaştırır.

- _Örnek:_ `ev/salon/sicaklik` veya `fabrika/motor1/devir_hizi`
    
- Tüketiciler belirli bir Topic'e abone olurken joker karakterler kullanabilir:
    
    - `+` (Artı): Sadece o seviyedeki her şeyi kapsar. (Örn: `ev/+/sicaklik` -> Hem salonun hem mutfağın sıcaklığını alır).
        
    - `#` (Kare): O seviyeden sonraki tüm alt başlıkları kapsar. (Örn: `ev/#` -> Evdeki tüm sensör verilerini alır).
        

### 2. <span style="color: rgb(235, 120, 129)"> QoS (Quality of Service - Hizmet Kalitesi) Seviyeleri </span>

MQTT'nin en çok sorulan ve en önemli özelliğidir. Ağın durumuna ve verinin kritiklik seviyesine göre 3 farklı teslimat garantisi sunar:

- **QoS 0 (At most once - En fazla bir kere):** "Ateşle ve unut". Üretici mesajı gönderir, ulaşıp ulaşmadığına bakmaz. Teyit (ACK) yoktur. (Örn: Her saniye gönderilen önemsiz bir rüzgar hızı verisi. Biri kaybolsa da olur, saniye sonra yenisi gelecek zaten.)
    
- **QoS 1 (At least once - En az bir kere):** Mesajın karşıya ulaştığı teyit edilene kadar tekrar gönderilir. Mesaj kesin ulaşır ama bazen yanlışlıkla iki kere (mükerrer) ulaşabilir. (Örn: Bir cihazın batarya seviyesi uyarısı.)
    
- **QoS 2 (Exactly once - Tam olarak bir kere):** En güvenli ama en yavaş yöntemdir. Mesajın sadece bir kez ve kesinlikle ulaştığından emin olmak için dört adımlı bir onay süreci işler. (Örn: Akıllı bir kilidi açma komutu. İki kere çalışmasını veya komutun kaybolmasını istemezsin.)
    

### 3.<span style="color: rgb(235, 120, 129)">  Last Will and Testament (LWT - Son İstek ve Vasiyet) </span>

Eğer bir sensör veya cihaz, pili bittiği veya ağı koptuğu için aniden (Broker'a haber veremeden) çevrimdışı olursa, Broker bu durumu fark eder. Cihaz ilk bağlandığında Broker'a bıraktığı "Eğer aniden koparsam, şu Topic'e şu mesajı yayınla" vasiyetini devreye sokar. (Örn: "Sensör_X bağlantısı koptu" uyarısı göndermek).

### 4.  <span style="color: rgb(235, 120, 129)">Retained Messages (Kalıcı Mesajlar) </span>

Normalde Pub/Sub sistemlerinde, sen abone olmadan önce yayınlanan mesajları kaçırırsın. Ancak MQTT'de bir mesaja "Retained" bayrağı eklersen, Broker o Topic için gönderilen **en son mesajı** hafızasında tutar. Yeni bir cihaz o Topic'e abone olduğunda, hemen o son durumu (örneğin akıllı lambanın o anki "açık/kapalı" durumunu) öğrenir.

### <span style="color: rgb(130, 232, 127)"> MQTT'nin Avantajları </span>

- Bant genişliğini (internet kotasını) çok az kullanır, paket başlıkları (header) sadece birkaç byte boyutundadır.
    
- Cihazların pilini çok az tüketir.
    
- Bağlantı koptuğunda durumu yönetmek için harika dahili mekanizmaları (QoS, LWT) vardı



---

