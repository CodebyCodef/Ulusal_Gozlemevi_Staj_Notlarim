
**???**



```txt
İME sonunda sorumlu öğretim üyesi ve 3 bölüm öğretim üyesinden oluşacak 4 kişilik komisyon önünde yapacağınız sunum üzerinden komisyon sizi aşağıdaki başlıklarda değerlendirecektir. 

•Sunumun içeriğinin İME deneyimini ve sektörü açıklama yönünden yeterliliği ve sunum esnasındaki iletişim becerisi 

•İş yerinde yapılan işleri anlama, kavrama ve kazanım elde edilme düzeyi 

•İş yerinde aktif görev alma, problemlere mühendis bakış açısıyla çözüm üretebilme düzeyi 

•Teorik bilgiyi pratikle ilişkilendirebilme becerisi •İME yapılan sektör ile ilgili sahip olunan bilgi birikimi düzeyi

•İME dosyasındaki içeriğin niteliği, dosya şablon
```
## Ana başlıklar

### 1. Giriş

- Kendini Tanıt 
	- İsim 
	- Soyisim

- Stajı nerede yaptın ? 
	- Türkiye Ulusal Gözlemevleri Merkez Ofisi (DAG400 yerleşkesinin merkezi binası eski ATASAM)
	- Hangi birim?
		- Yazılım / AR-GE
	- Sorumlu Mühendisin kim?
		- Emrullah KUŞTAŞI

- Kurum hakkında biraz bilgi verir misin?
	- DAG400 (Teleskop çalışması hakkında)
		- Optik çalışmaları ve yurt dışından gelen ekibin yapmış olduğu çalışmalar (Nazmit )
	- Temel hareket kontrolleri ve yazılım yerelleştirme hk.
	- Ar-Ge faaliyetleri
	- OPAL (Kaplama Ünite Projeleri ve Yeni Kurum Binası)

- Kurumda yaptığınız veya dahil olduğun projeler hakkında bilgi verir misin?

	- **Personel Yönetim Sistemi Web Uygulaması:** FastAPI, PostgreSQL ve Docker kullanılarak geliştirilen, kullanıcı profil resmi ekleme gibi fonksiyonları barındıran backend projesi.
		- ORM based development
		- multi-person connections via PC's
    
	- **Mobil Uygulama (ReadableLib / E-Kitap Okuyucu):** Flutter tabanlı olarak geliştirilen, kitap okuma takibi, ortak çalışma alanı (Collab Workspace) ve PDF işleme mimarisi içeren mobil uygulama projesi.
		- Kişisel boş zamanlar da AI ile birlikte geliştirmiş olduğum okuma productivity uygulaması
		- Amaç PDF olarak edinilen kitapların EPUB dönüşümlerini olabilecek en iyi şekilde sağlayarak performanslı bir kitap okuma deneyemi sunabilmek.
    
	- **Akıllı Priz Yerel Kontrol Sistemi:** DAG400 yerleşkesindeki akıllı prizlerin (HS110, P100, P110) yerel ağ üzerinden yönetimi için MQTT protokolü ve REST API kullanılarak geliştirilen, "Plugin" mimarisiyle desteklenen kontrol sistemi.
		- Tp-Link markalı akıllı prizlerin yönetimlerini kurumsal uygulama ile kullanmak yerine reverse engineering ile elde edilmiş API bilgileri ve cihaz bağlantısı ile birlikte özel bir arayüz bağlantısı ile birlikte sağlamak.
    
	- **TUG Yıldız Haritası Web Sitesi:** Astronomik konum ve çizgi verilerinin (JSON formatında) işlenerek takımyıldızlarının web ortamında görselleştirilmesini sağlayan Python ve JavaScript tabanlı kişisel proje.
		- TUG ait site de eksik olduğunu düşündüğüm AI ile kısa sürede yapmış olduğum Yıldız Haritası Sitesi. GitHub io ile birlikte yayında durmakta sorumlu mühendis belki kullanabilir (_?_)
    
	- **TUG Enter Projesi:** Fiziksel bir donanım olan "büyük sünger Enter butonu"nun yazılım sistemiyle entegre edilerek, Docker üzerinden dağıtımının yapıldığı ofis içi proje.
		- Sorumlu mühendisin odasında bulunan sünger ENTER tuşunun (aslında normal Enter tuşu ile aynı işleve ait) bağlı şekilde geliştirilmiş olan proje oluşturma,saklama,silme ve bu oluşturma,saklama işlemlerine ek kolaj fotoğraf ekleme ve paydaş ekleyebilme özelliklerinin bulunduğu bir web site. İlgili web site Mustafa tarafından docker container ile birlikte saklanıp sonrasında hocaya teslim edildi (_?_) 
    
	- **Makita BL1830 Batarya Projesi:** Şarjlı matkap bataryasının BMS (Batarya Yönetim Sistemi) üzerindeki "LOCKED" (Kilitli) durumunu tersine mühendislik ve Arduino Nano kullanarak çözmeye odaklanan donanım müdahale ve haberleşme projesi.
		- Hakkı abinin bize lehim işlemini gerçekleştirmiş olduğu Arduino kitine uygulaması üzerinden kod iliştirme işlemini yaparak sonrasında bataryaya bağlayıp batarya kilidini açmaya çalıştık. (Burada seri iletişim protokelleri hakkında biraz araştırma yapmak gerekiyor bahsedebilmek için çünkü batarya bağlantılarına uçlar takarak sinyal iletmeye çalıştık.)
    
	- **BIST Hisse Takip Uygulaması:** Borsa İstanbul'da işlem gören 20 pilot şirketin verilerini, MACD ve RSI gibi teknik sinyaller eşliğinde anlık analiz edip izleyen finansal web uygulaması.
		- Bu proje Yandex üzerinden bilgi alan bir sistem ama bundan bahsetsem mi bahsetmesem mi bilmiyorum (Yandex olarak hatırlıyorum.)
    
	- **Act_Tracker (Yapay Zeka Destekli Web Analitik Platformu):** Web sitelerindeki kullanıcı davranışlarını (reklam performansı, sayfa etkileşimi) loglayan, görselleştiren ve OpenRouter API ile yapay zeka destekli analizler sunan SaaS platformu.
	    - İlk SaaS denemem oldu ama çalışma durumunu pek beğenmedim. Açıkcası API oluşturma bunu siteye entegre etme işlemlerine uygun bir web site ve test aşamalarını güzel şekilde yapamamıştım ama fikir fena değil kullanılabilir hala 
	    
	- **Weather App (Telegram Hava Durumu Botu):** API entegrasyonu ile geliştirilen ve @hava_nasil_bot adıyla aktif edilen hava durumu bilgilendirme sistemi.
		- Telegram API kullanımı hakkında bilgi sahibi oldum. Sabah 07.00 saatine ayarlı şekilde rutin hava durumu bilgisi ve ingilizce şekilde hava durumu ile ilgili olacak şekilde nasıl kıyafet giyilmesi için bir bilgi veriyor. (Metin içerisinde alt alta yani)
    
	- **Cloud Detection for DAG (Doğu Anadolu Gözlemevi İçin Bulut Tespiti):** Tüm Gökyüzü Kamerası'ndan (ASC) elde edilen astronomik FITS görüntülerinin, HOG öznitelik çıkarımı ve Makine/Derin Öğrenme modelleri (SVM, KNN, CNN) kullanılarak analiz edildiği Ar-Ge görüntü işleme projesi.
		- Bu proje 7-8 yıl önce yapılmış aslında güzel içeriklere ve DAG konumuna uygun olacak şekilde maskeleme yapabilmekte fakat bu konu bana çok yabancı şuanda "fits" ve "HOG" hakkında çalışma yapıyorum. Bu proje çalışmasına yardımcı olacak şekilde 1 adet FITS dosyalı "cloudynight" projesi ve 818 png görüntülü "Almeira" verisetine uyarlanmış bir .ipynb dosyası oluşturdum. Burada "Cloud Detection for DAG" projesinde bulunan maskeleme tekniklerine bakacağım. Kendi örneklerimi de anlatacağım. (Kalman Filtresi hk. bak!!!)
    
	- **OWASP Top 10 Güvenlik Test Projesi:** Eğitim amaçlı olarak PHP ve HTML ile kodlanan, SQL Injection ve URL Injection gibi zafiyetlerin "güvensiz" ve "güvenli" kod senaryolarını barındıran proje.
		- Burada ki örnekler tamamıyla AI based. Amaç öğretmek zaten. çok bahsetmeden geçersin yaptım ettim diye.
    
	- **OAuth 2.0 ve Keycloak Demo Uygulamaları:** Merkezi kimlik yönetimi mekanizmalarını test etmek amacıyla kurulan Keycloak sunucusu ve "Google ile Giriş Yap" (Authorization Code Flow) simülasyonu içeren demo projesi.
		- Burada Keycloak'a ait IAM admin hakkında Realm ve Client bağıntılarını belki .md file içerisinde anlattığın gibi şekillendirerek ufak bir bahsetme sağlanabilir.
    
	- **Proje Başvuru ve İnceleme Sistemi:** Kurumun operasyonel ihtiyaçları doğrultusunda değerlendirme toplantısı yapılan, kimlik yönetimi ve dosya depolama altyapısı tasarlanan proje.
		- Bu proje sadece ama sadece fikir üzerinde kaldı ve tartışıldı üzerine herhangi bir kod yazma ya da proje oluşturmaya başlama işlemi olmadı. 1 cümle ile bahsedilebilir ya da boşver.

	- SUNUMLAR :D
		- Composite Design Pattern
		- CQRS - CORS
		- Factory Design Pattern
		- ORM Mimarisi
		- Shallow Copy & Deep Copy
		- OWASP TOP 10
		- OpenAuth - OpenID - Keycloak