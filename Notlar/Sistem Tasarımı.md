

# IAAS, PAAS, SAAS ve SSO Konu Anlatımı

## Giriş

Bulut bilişim (Cloud Computing), donanım ve yazılım kaynaklarının internet üzerinden servis olarak sunulmasını sağlar. Günümüzde uygulama geliştirme, veri yönetimi ve kullanıcı kimlik doğrulama süreçleri büyük ölçüde bulut teknolojileri ile yürütülmektedir.

Bu dokümanda aşağıdaki kavramlar detaylı şekilde ele alınacaktır:

- IAAS (Infrastructure as a Service)
    
- PAAS (Platform as a Service)
    
- SAAS (Software as a Service)
    
- SSO (Single Sign-On)
    

---

# IAAS (Infrastructure as a Service)

## IAAS Nedir?

Infrastructure as a Service (Altyapı Hizmeti), kullanıcıya sanal sunucu, ağ, depolama ve işlem gücü gibi temel altyapı bileşenlerini internet üzerinden sunan bulut hizmet modelidir.

Bu modelde kullanıcı:

- Sunucu yönetimini yapabilir
    
- İşletim sistemi kurabilir
    
- Ağ yapılandırması gerçekleştirebilir
    
- Uygulamalarını istediği gibi deploy edebilir
    

Fiziksel donanım yönetimi ise servis sağlayıcı tarafından gerçekleştirilir.

---

## IAAS Mimarisi

IAAS yapısında genel olarak şu bileşenler bulunur:

1. Fiziksel Sunucular
    
2. Hypervisor / Sanallaştırma Katmanı
    
3. Sanal Makineler (VM)
    
4. Ağ Yapısı
    
5. Depolama Servisleri
    
6. Yönetim Paneli
    

PDF içerisinde anlatılan sanallaştırma konusu IAAS altyapısının temelini oluşturur.

---

## Sanallaştırma (Virtualization)

PDF içerisinde VMware ve Docker karşılaştırması üzerinden sanallaştırma anlatılmıştır.

Sanallaştırma:

- Tek fiziksel sunucu üzerinde birden fazla işletim sistemi çalıştırılmasını sağlar.
    
- Hypervisor kullanılır.
    
- Her sanal makine kendi işletim sistemine sahiptir.
    

### Avantajları

- Kaynak paylaşımı
    
- Yüksek izolasyon
    
- Sunucu maliyetlerini azaltma
    
- Kolay ölçeklenebilirlik
    

### Dezavantajları

- Container yapısına göre daha ağırdır
    
- Daha fazla RAM ve CPU tüketebilir
    

---

## Containerization ve IAAS İlişkisi

PDF içerisinde Docker container yapısının sanallaştırmadan daha hafif olduğu belirtilmektedir.

Container yapısı:

- İşletim sistemi seviyesinde sanallaştırma yapar
    
- Hypervisor ihtiyacını azaltır
    
- Daha hızlı başlatılır
    
- Daha az kaynak tüketir
    

Bu yapı modern IAAS sistemlerinde yoğun şekilde kullanılmaktadır.

---

## IAAS Örnekleri

### Amazon Web Services (AWS)

- EC2
    
- EBS
    
- VPC
    

### Microsoft Azure

- Azure Virtual Machines
    
- Azure Storage
    

### Google Cloud Platform

- Compute Engine
    
- Persistent Disk
    

---

## IAAS Avantajları

- Esnek yapı
    
- Tam kontrol
    
- Yüksek ölçeklenebilirlik
    
- Donanım maliyetlerini azaltır
    
- Otomasyon desteği sağlar
    

---

## IAAS Dezavantajları

- Yönetim karmaşıktır
    
- Güvenlik yönetimi kullanıcıya aittir
    
- Sistem yönetimi bilgisi gerekir
    

---

# PAAS (Platform as a Service)

## PAAS Nedir?

Platform as a Service modeli, geliştiricilere uygulama geliştirme ve deploy etme ortamı sağlayan bulut hizmet modelidir.

Bu modelde:

- Sunucu yönetimi servis sağlayıcı tarafından yapılır
    
- Kullanıcı yalnızca uygulama geliştirmeye odaklanır
    
- Runtime ortamı hazır gelir
    

PAAS modeli özellikle yazılım geliştirme ekipleri için büyük kolaylık sağlar.

---

## PAAS Özellikleri

- Hazır runtime ortamı
    
- Otomatik ölçekleme
    
- Veritabanı entegrasyonu
    
- CI/CD desteği
    
- Monitoring araçları
    
- API yönetimi
    

---

## Serverless ve PAAS

PDF içerisinde AWS Lambda anlatılmaktadır.

AWS Lambda modern PAAS/serverless yaklaşımının önemli örneklerinden biridir.

Lambda sistemi:

- Olay tetiklemeli çalışır
    
- Sunucu yönetimi gerektirmez
    
- Otomatik ölçeklenebilir
    
- Kullanım kadar ücretlendirme sağlar
    

PDF içerisinde Lambda'nın Firecracker MicroVM yapısı kullandığı belirtilmektedir.

---

## PAAS Kullanım Alanları

- Web uygulamaları
    
- REST API servisleri
    
- Mikroservis mimarileri
    
- Mobil backend sistemleri
    
- Event-driven uygulamalar
    

---

## PAAS Örnekleri

### Google App Engine

Kod deploy ederek uygulama çalıştırılmasını sağlar.

### Heroku

Geliştiricilerin hızlı şekilde uygulama yayınlamasını sağlar.

### AWS Elastic Beanstalk

AWS üzerinde uygulama deploy yönetimi sağlar.

### Azure App Services

Microsoft ekosistemi ile entegre çalışır.

---

## PAAS Avantajları

- Hızlı geliştirme süreci
    
- Daha az sistem yönetimi
    
- Otomatik ölçeklenebilirlik
    
- Geliştirici verimliliği
    

---

## PAAS Dezavantajları

- Altyapı kontrolü sınırlıdır
    
- Vendor lock-in oluşabilir
    
- Özelleştirme kısıtlı olabilir
    

---

# SAAS (Software as a Service)

## SAAS Nedir?

Software as a Service modeli, doğrudan son kullanıcıya internet üzerinden yazılım hizmeti sunar.

Kullanıcı:

- Uygulama kurmaz
    
- Güncelleme yapmaz
    
- Altyapı yönetmez
    
- Sadece uygulamayı kullanır
    

Tüm yönetim servis sağlayıcı tarafından gerçekleştirilir.

---

## SAAS Özellikleri

- Tarayıcı üzerinden erişim
    
- Merkezi yönetim
    
- Otomatik güncelleme
    
- Çok kullanıcılı yapı (multi-tenant)
    
- Abonelik tabanlı kullanım
    

---

## SAAS Örnekleri

### Google Workspace

- Gmail
    
- Google Docs
    
- Google Drive
    

### Microsoft 365

- Outlook
    
- Word Online
    
- Teams
    

### Slack

Takım iletişimi için kullanılan SAAS platformudur.

### Zoom

Online toplantı hizmeti sunar.

---

## SAAS Avantajları

- Kolay kullanım
    
- Kurulum gerektirmez
    
- Düşük başlangıç maliyeti
    
- Hızlı erişim
    
- Otomatik güncellemeler
    

---

## SAAS Dezavantajları

- Veri kontrolü sınırlıdır
    
- İnternet bağımlılığı vardır
    
- Özelleştirme sınırlı olabilir
    

---

# IAAS vs PAAS vs SAAS

|Özellik|IAAS|PAAS|SAAS|
|---|---|---|---|
|Yönetim Seviyesi|Altyapı|Platform|Yazılım|
|Kullanıcı Kontrolü|Yüksek|Orta|Düşük|
|Teknik Bilgi Gereksinimi|Yüksek|Orta|Düşük|
|Kullanım Amacı|Sistem yönetimi|Uygulama geliştirme|Son kullanıcı hizmeti|
|Örnek|AWS EC2|Heroku|Gmail|

---

# SSO (Single Sign-On)

## SSO Nedir?

Single Sign-On (Tek Oturum Açma), kullanıcının bir kez kimlik doğrulaması yaparak birden fazla sisteme erişebilmesini sağlayan kimlik doğrulama yöntemidir.

Kullanıcı:

- Tek kullanıcı adı ve şifre kullanır
    
- Bir kez giriş yapar
    
- Birden fazla uygulamaya tekrar giriş yapmadan erişebilir
    

---

## SSO Nasıl Çalışır?

Temel çalışma mantığı:

1. Kullanıcı giriş ekranına gider
    
2. Kimlik doğrulama sunucusuna yönlendirilir
    
3. Kullanıcı doğrulanır
    
4. Token oluşturulur
    
5. Kullanıcı diğer sistemlere token ile erişir
    

PDF içerisinde token-based authentication mantığı anlatılmıştır.

---

## Token Based Authentication

PDF içerisinde token tabanlı doğrulama şu şekilde açıklanmıştır:

1. Kullanıcı giriş bilgilerini Authentication Server'a gönderir
    
2. Sunucu kullanıcıyı doğrular
    
3. Expire süresine sahip token üretir
    
4. Client her istekte token gönderir
    
5. Sunucu token doğrulaması yapar
    

Bu yapı modern SSO sistemlerinin temel yapı taşlarından biridir.

---

## SSO Protokolleri

### OAuth 2.0

Yetkilendirme protokolüdür.

Kullanıcının kaynaklarına kontrollü erişim sağlar.

---

### OpenID Connect (OIDC)

OAuth 2.0 üzerine kimlik doğrulama katmanı ekler.

Modern uygulamalarda yaygın şekilde kullanılır.

---

### SAML

Kurumsal sistemlerde kullanılan XML tabanlı kimlik doğrulama standardıdır.

---

## SSO Avantajları

- Kullanıcı deneyimini artırır
    
- Tek parola yönetimi sağlar
    
- Güvenlik politikalarını merkezileştirir
    
- Yönetim kolaylığı sağlar
    

---

## SSO Dezavantajları

- Merkezi sistem arızası tüm erişimleri etkileyebilir
    
- Tek hesabın ele geçirilmesi büyük risk oluşturur
    
- Doğru yapılandırma gerektirir
    

---

# SSO ve Modern Kimlik Yönetimi

Modern sistemlerde SSO çözümleri genellikle şu araçlarla birlikte kullanılır:

- Keycloak
    
- Auth0
    
- Okta
    
- Azure Active Directory
    
- Google Identity
    

Bu sistemler:

- OAuth2
    
- OpenID Connect
    
- JWT
    
- Multi-Factor Authentication (MFA)
    

teknolojilerini birlikte kullanır.

---

# Mikroservisler ve Kimlik Yönetimi

PDF içerisinde mikroservis mimarilerinden bahsedilmektedir.

SSO sistemleri mikroservis mimarilerinde oldukça önemlidir.

Çünkü:

- Birden fazla servis bulunur
    
- Merkezi authentication gerekir
    
- Token yönetimi gerekir
    
- API Gateway doğrulama yapabilir
    

Bu yapı sayesinde tüm servisler merkezi kimlik sistemi ile çalışabilir.

---

# CDN, Cache ve Cloud Yapıları

PDF içerisinde CDN, caching ve dağıtık sistem mimarileri anlatılmıştır.

Cloud sistemlerinde:

- CDN performans artırır
    
- Cache veri erişimini hızlandırır
    
- Load balancer trafiği dağıtır
    
- Horizontal scaling sistem büyümesini sağlar
    

Bu bileşenler IAAS, PAAS ve SAAS sistemlerinde yoğun şekilde kullanılmaktadır.

---

# Sonuç

IAAS, PAAS ve SAAS bulut bilişimin temel servis modelleridir.

- IAAS altyapı sağlar
    
- PAAS geliştirme platformu sağlar
    
- SAAS doğrudan yazılım hizmeti sunar
    

SSO ise modern uygulamalarda merkezi kimlik doğrulama sağlayarak kullanıcı deneyimini ve güvenliği artırır.

Modern yazılım mimarilerinde:

- Cloud Computing
    
- Mikroservisler
    
- Token Authentication
    
- OAuth2
    
- OpenID Connect
    
- Containerization
    
- Serverless
    

kavramları birlikte kullanılmaktadır.

Bu yapıların doğru anlaşılması modern backend, DevOps ve sistem tasarımı süreçleri açısından oldukça önemlidir.