

## 1. HTTP İletişiminin Temelleri (Headers)

Bir web sitesine bağlandığınızda, tarayıcınız sunucuya "HTTP Header" adı verilen başlık bilgileri gönderir. Bu bilgiler, isteğin "zarfı" üzerindeki notlar gibidir.

  ```http
GET /api/user/profile HTTP/1.1

Host: www.ornek-site.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36
Accept: application/json
Accept-Language: tr-TR,tr;q=0.9,en-US;q=0.8
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...
  ```

* **User-Agent:** Cihazın işletim sistemi, işlemci mimarisi ve tarayıcı sürümünü belirtir.

* **Accept-Language:** Kullanıcının tercih ettiği dil (örn: `tr-TR`). Konum tahmini için ilk ipucudur.

* **Host:** İsteğin hangi alan adına (domain) gittiğini belirtir.

* **Authorization:** Kullanıcının kimliğini kanıtlayan token bilgisini (genellikle `Bearer` prefix'i ile) taşır.
 
  

---

  

## 2. Token Yapısı ve İçeriği (JWT)

Kimlik doğrulama için kullanılan JSON Web Token (JWT) gibi yapılar, kendi içlerinde belirli "Claim" (beyan) anahtar kelimeleri barındırır.

  ```json
  {
  "sub": "104523",
  "name": "Ahmet Yılmaz",
  "email": "ahmet@ornek.com",
  "role": "premium_user",
  "iat": 1714371600,
  "exp": 1714375200
  }
  ```

* **sub (Subject):** Kullanıcının sistemdeki benzersiz ID'si.

* **iat (Issued At):** Token'ın oluşturulma zamanı.

* **exp (Expiration Time):** Token'ın geçerliliğinin sona ereceği zaman.

* **role/scopes:** Kullanıcının sahip olduğu yetki seviyeleri (admin, user vb.).

* **Custom Fields:** Geliştirici tarafından eklenen özel veriler (örn: `last_city`).

  

---


## 3. Web Siteleri Konumu Nasıl Algılar?

Sistemler konum tespiti için iki temel mekanizma kullanır:

  

### A. IP Adresi Üzerinden Tahmin (Pasif Yöntem)

* **<span style="color:rgb(0, 112, 192)">Mantık</span>:** Her internet bağlantısının bir IP adresi vardır. Sunucu, bu IP adresini devasa coğrafi veritabanları (Geo-IP Databases) ile eşleştirir.

* **<span style="color:rgb(0, 112, 192)">Doğruluk</span>:** Şehir veya bölge düzeyindedir. Kesin adres vermez.

* **<span style="color:rgb(0, 112, 192)">Veri</span> <span style="color:rgb(146, 208, 80)"><span style="color:rgb(0, 112, 192)">Akışı</span></span>:** IP adresi, bağlantının doğası gereği sunucuya her zaman iletilir.

  

### B. Geolocation API (Aktif Yöntem)

* <span style="color:rgb(146, 208, 80)">Mantık</span>: Tarayıcı (Chrome/Safari), cihazın GPS, Wi-Fi ve baz istasyonu verilerini kullanır.

* **<span style="color:rgb(146, 208, 80)">İzin Mekanizması</span>:** Kullanıcıdan açık rıza (pop-up) alınması zorunludur.

* **<span style="color:rgb(146, 208, 80)">Veri Akışı</span>:** Tarayıcı, elde ettiği kesin koordinatları (Enlem/Boylam) JavaScript aracılığıyla sunucuya bir veri paketi olarak gönderir.


```json 
{
  "sub": "104523",
  "role": "user",
  "last_known_city": "Erzurum",
  "lat": 39.9042,
  "lon": 41.2679
}
```
  

---

  

## 4. VPN ve Konum Yanılsaması

VPN kullanıldığında, web sitelerinin konumunuzu yanlış algılamasının teknik nedeni şudur:

  

1.  **Maskeleme:** VPN, isteğinizi kendi sunucusu üzerinden yönlendirir.

2.  **IP Değişimi:** Web sitesinin sunucusu, sizin gerçek IP'nizi değil, VPN sunucusunun (örneğin Almanya'daki bir sunucu) IP'sini görür.

3.  **Otomatik Yerelleştirme:** Site sunucusu, IP adresinin ait olduğu ülkeye bakarak dili, para birimini ve içeriği otomatik olarak o bölgeye göre günceller.

  

---

  
## Özet Akış Şeması

1. **İstek Yapılır** -> 2. **IP Adresi & Headerlar İletilir** -> 3. **Sunucu IP'den Şehir Tahmini Yapar** -> 4. **Eğer İzin Verilirse GPS ile Kesin Konum Alınır** -> 5. **Tüm Bu Veriler İşlenerek Kullanıcıya Özel İçerik Sunulur.**