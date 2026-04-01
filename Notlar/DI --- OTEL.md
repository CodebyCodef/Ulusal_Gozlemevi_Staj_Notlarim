( Dependency Injection ) --- ( OpenTelemetry )
# Dependect Injection Nedir?

- Bir nesnenin ihtiyaç duyduğu parçaları (bağımlılıkları) kendi içinde üretmesi yerine, dışarıdan almasıdır.

```python 
class Pil:
	def enerji_ver(self):
		return "Standart Pil Enerjisi"
		

class Gamepad:
	def __init__(self):
		self.pil = Pil()
		
	def calis(self):
		print(self.pil.enerji_ver())
		
		

## Burada Gamepad sınıfı, Pil sınıfına bağımlıdır ve onu kendi içinde yaratır. Değiştirmek imkansızdır.
```

```python
class Gamepod:
	def __init__(self, enerji_kaynagi):
		self.guc_kaynagi = enerji_kaynagi
		
	def calis(self):
		print(self.guc_kaynagi.enerji_ver())
		
standart_pil = Pil()
sarjli_pil = SarjliPil()

benim_kol = Gamepad(standart_pil)
arkadas_kol = Gamepad(sarjli_pil)

## Burada Gamepad sınıfı, Pil sınıfına bağımlı değildir ve istenen türler gönderilebilir.
```


## DI (dependecy injection) Neden Kullanılır?

1.  __Gevşek Bağlılık (Loose Coupling):__ Parçalar birbirine japon yapıştırıcısı ile değil, vida ile bağlıdır. İstediğin zaman söküp takabilirsin.
2.  __Kod Tekrarını Önler:__ Veritabanı bağlantısını tek bir yerde tanımlarsın, her yerde kullanırsın.
3. __Test Edilebilirlik (!!!!!!!!!):__ Gerçek veritabanı yerine "Sahte (Mock) Veritabanı" enjekte edip, s,stem, bozmadan test yapabilirsin.


--- 


# OpenTelemetry (OTEL) Nedir? 

- OTEL, sisteme giren her isteğe bir Takip Cihazı (Trace ID ) takar. Bu cihaz, istek nereye direse gitsin (REST -> gRPC -> DB) onu takip eder.


| Adım(Span)              | Geçen Süre | Durum         |
| ----------------------- | ---------- | ------------- |
| **Toplam İstek**        | **250 ms** | **Başarılı**  |
| 1. REST API İsteğe Aldı | **10 ms**  | **Başarılı**  |
| 2. gRPC Çağrısı Yaptı   | **5 ms**   | **Başarılı**  |
| 3. Veritabanı Kaydı     | **230 ms** | **! YAVAŞ !** |
| 4. Cevap Döndü          | **5 ms**   | Başarılı      |

## OTEL'in 3 Temel Yapıtaşı

1.  __Traces (İzler):__ İsteğin yolculuğu. "Kim kimi çağırdı?"
2.  __Metrics (Metrikler):__ Sayısal veriler. "Şuan sunucuda CPU kullanımı % kaç?" , "Son 1 saatte kaç hata aldık?"
3. __Logs (Kayıtlar):__ Yazılı mesajlar. "Hata oluştu: Bağlantı koptu"


KULLANICI (Browser)
    |
    |  (1. İstek Geldi: "Ürün Ekle")
    v
+-----------------------+
|  🖥️  FastAPI (REST)   | <--- 🕵️ OTEL BURADA BAŞLATIR
+-----------------------+      (Barkod: 12345)
    |                          (Kronometre Başladı: 00:00)
    |
    |  (2. İstek gRPC'ye gidiyor... Barkod hala üzerinde!)
    v
+-----------------------+
|  ⚡  gRPC Sunucusu    | <--- 🕵️ OTEL BURADA DEVAM EDER
+-----------------------+      (Barkod: 12345 - Kontrol edildi)
    |                          (Ara Süre Kaydedildi)
    |
    |  (3. Veritabanına yazılıyor...)
    v
+-----------------------+
|  🗄️  SQLite (DB)      | <--- 🕵️ OTEL BURADA BİTİRİR
+-----------------------+      (İşlem bitti. Toplam Süre: 200ms)


---

!!! CQRS

CORS

!!! Mediator

İlgili konuların detaylarına bak. 

Tasarım Mimarisi
Gereksinimlerin mimariye aktarılması

Clean Architecture
Hexagonal Architecture
N Katmanlı Mimari

Her bir iş için öncelikle Core tanımlaması olacak ( Detaylı yazılım bilgileri haricinde yapılacak işler sonucu )



