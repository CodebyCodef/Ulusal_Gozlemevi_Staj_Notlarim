# Open Web Application Security Project 


1. [A01:2025 - Broken Access Control](https://owasp.org/Top10/2025/A01_2025-Broken_Access_Control/)
2. [A02:2025 - Security Misconfiguration](https://owasp.org/Top10/2025/A02_2025-Security_Misconfiguration/)
3. [A03:2025 - Software Supply Chain Failures](https://owasp.org/Top10/2025/A03_2025-Software_Supply_Chain_Failures/)
4. [A04:2025 - Cryptographic Failures](https://owasp.org/Top10/2025/A04_2025-Cryptographic_Failures/)
5. [A05:2025 - Injection](https://owasp.org/Top10/2025/A05_2025-Injection/)
6. [A06:2025 - Insecure Design](https://owasp.org/Top10/2025/A06_2025-Insecure_Design/)
7. [A07:2025 - Authentication Failures](https://owasp.org/Top10/2025/A07_2025-Authentication_Failures/)
8. [A08:2025 - Software or Data Integrity Failures](https://owasp.org/Top10/2025/A08_2025-Software_or_Data_Integrity_Failures/)
9. [A09:2025 - Security Logging and Alerting Failures](https://owasp.org/Top10/2025/A09_2025-Security_Logging_and_Alerting_Failures/)
10. [A10:2025 - Mishandling of Exceptional Conditions](https://owasp.org/Top10/2025/A10_2025-Mishandling_of_Exceptional_Conditions/)

--- 
# 1. Broken Acces Control 


- Bir kullanıcının erişmemesi gereken bilgilere (veri, API, sayfa vb.) yetkisiz şekilde erişip işlem yapmasıdır.

Gerçek hayat üzerinde;
- Admin paneline erişim
	- Başka kullanıcılara ait verileri görmek
	- Yetkisiz işlem yapmak
	- Para transferi
	- Sipariş Manipülasyonu

Yaygın sebepleri;
- Backend üzerinde authorization eksiklikleri
- JWT tokenlerinde role uygun olmayan kontrol hataları
- API endpointlerinde validation eksiklikleri

Önlemler;
- Backend authorization kontrolleri

```python
	  #Yanlış
	  if isLoggendIn:
	  
	  #Doğru
	  if user.id == request.id
	  ```


```

- RBAC (Role Based Access Control)
	- admin
	- user
	- moderator

- LPP (Least Privilege Principle)
	- Kullanıcıya verilebilecek minimum yetkiyi verme işlemidir.


---

# 2. Security Misconfiguration

- Sistemlerin yanlış ayarlanması , default bırakılması, gereksiz açık servisler barındırmasıdır. 


Gerçek hayatta;
- Default admin şifresi
- Açık debug modu
- Gereksiz portlar
- Hataların client (kullanıcı) tarafında gösterilmesi
- Yanlış CORS ayarları

Alınabilecek önlemler;
- **Hardened configuration** (Bir sistemin, yazılımın veya ağın saldırı yüzeyini en aza indirmek için yapılan güvenlik iyileştirmeleridir. Fabrika ayarları genellikle kullanım kolaylığı için birçok özelliği açık bırakır; "hardening" ise bu kapıları kapatma sürecidir.)

- Production üzerinde debug kapatmak

-  **Güvenli headerlar** (Tarayıcılar bu başlıkları okuyarak sitenizi XSS (Cross-Site Scripting), Clickjacking ve veri hırsızlığı gibi yaygın saldırı türlerine karşı otomatik olarak koruma altına alır.)


---

# 3. Software Supply Chain Failures

- Projede kullanılan:
	- third-party package’lar
	- dependency’ler
	- CI/CD pipeline
	- build süreçleri

üzerinden saldırı yapılmasıdır.

Gerçek hayatta;

- **SolarWinds Attack** ;

	- Saldırganlar (genellikle Rusya bağlantılı APT29 veya Nobelium grubu olduğu belirtilir), SolarWinds şirketinin ağ yönetim yazılımı olan **Orion**'un yazılım geliştirme hattına sızdılar.

	- **Truva Atı Güncellemesi:** Saldırganlar, Orion yazılımının resmi güncellemelerine gizlice zararlı bir kod (malware) yerleştirdiler.
	    
	- **Güven İstismarı:** Yazılım, SolarWinds tarafından dijital olarak imzalandığı için müşteriler bu güncellemeyi "güvenilir" olarak gördü ve sistemlerine kurdu.
	    
	- **Uyku Modu:** Zararlı kod, sisteme girdikten sonra fark edilmemek için yaklaşık 2 hafta boyunca hiçbir işlem yapmadan bekledi.
	    
	- **18.000 Kurban:** SolarWinds'in 33.000 müşterisinden yaklaşık 18.000'i bu zehirli güncellemeyi indirdi.
	    
	- **Üst Düzey Hedefler:** Saldırıya uğrayanlar arasında ABD Hazine Bakanlığı, Enerji Bakanlığı, Pentagon ve Microsoft, FireEye gibi teknoloji devleri bulunuyordu.
	    
	- **Veri Sızıntısı:** Saldırganlar, aylarca bu ağlarda sessizce gezindi, e-postaları okudu ve hassas verileri dışarı sızdırdı.


Alınabilecek Önlemler;
- Dependecy scanning (Dependabot, Snyk, Trivy)
- Package pinning


---

# 4. Cryptographic Failures

- Şifreleme süreçlerinin:

	- yanlış uygulanması,
	- eksik uygulanması,
	- eski algoritmalar kullanılmasıdır.


Örnekler;

- HTTP kullanımı
- MD5 hash
- Weak JWT secret
- Plaintext password


```python
#Yanlış
password = "123efe"

#Doğru
bcrypt.hashpw(password) #hashleme işlemi
```


Önlemler;
- HTTPS zorunlu kılmak (modern ==> AES-256, bcrypt, Argon2)
- Secret management (.env, vault)


--- 


# 5. Injection

- Kullanıcı girdisinin:

	- SQL,
	- NoSQL,
	- command,
	- LDAP

gibi interpreter’lara kontrolsüz verilmesidir.


Örnek;

```python
#Yanlış
query = f"SELECT * FROM users WHERE id={user_input}"

# Burada girdi olarak id==1 OR 1=1 girişi yapılırsa sisteme erişilerek tüm kullanıcı bilgilerine erişilebilir.

#Doğru
cursor.execute(
 "SELECT * FROM users WHERE id=%s",
 (user_id,)
)

# Sorgu içerisinde veritbanı tarafına gönderilecek bilginin metin olarak beklenmesi sağlanıyor. Dolayısıyla çalıştırılabilir sorguların önüne geçilmiş oluyor.

```


Önlemler;
- ORM mimari kullanımı (SQLAlchemy, Django ORM)
- Input validation


--- 


# 6. Insecure Design

- Kod doğru olsa bile sistem mimarisinin güvenli tasarlanmamış olmasıdır.


Örnek;

- Şifre sıfırlama sistemi:

	- rate limit yok
	- token expiration yok

Kod hatasız olabilir.

Ama tasarım güvensizdir.


Tehlikeli Durumlar;

- **Abuse cases düşünülmemesi** 
	- **Abuse cases** (suistimal senaryoları), bir sistemin nasıl _kullanılması gerektiğini_ değil, kötü niyetli bir aktör tarafından nasıl _suistimal edilebileceğini_ modelleyen senaryolardır. "User Case" (Kullanıcı Senaryosu) ne yapılacağını anlatırken, Abuse Case sistemin sınırlarının nasıl zorlanacağını anlatır.
	
- Threat modeling eksikliği
	- **Threat Modeling (Tehdit Modelleme)**, bir sistemi henüz inşa etmeden veya yeni özellikler eklemeden önce "Burada ne ters gidebilir?" sorusunu sorma sürecidir.
	
- Business logic flaws
	- **Business Logic Flaws** (İş Mantığı Hataları), bir uygulamanın kodunda teknik bir açık (SQL Injection veya XSS gibi) olmamasına rağmen, tasarlanan iş akışındaki boşluklar nedeniyle kötüye kullanılmasıdır.


Önleme;

- Threat modeling

- Secure by Design yaklaşımı
	- **Secure by Design (Tasarım Gereği Güvenlik)**, güvenliği bir yazılım projesine sonradan eklenen bir "yama" veya "ek katman" olarak değil, projenin en başından, yani mimari ve tasarım aşamasından itibaren temel bir gereksinim olarak ele alma yaklaşımıdır.


--- 


# 7. Authentication Failures


- Kimlik doğrulama süreçlerindeki hatalardır.

 Örnekler;
- Weak password policy
- MFA olmaması
- Session fixation
- Credential stuffing


Önleme;

 - MFA kullan
- Strong password policy
- Rate limiting
- Secure session management


--- 


# 8. Software and Data Integrity Failures


- Kod veya verinin güvenilirliğinin doğrulanmamasıdır.

Örnekler;

- unsigned update
- insecure deserialization
- CI/CD compromise

Önleme;

- Integrity verification
- Signed updates
- Güvenli serialization
	- JSON tercih et


--- 


# 9. Security Logging & Alerting Failures


Saldırıların:

- loglanmaması,
- izlenmemesi,
- fark edilmemesi.


Örnek;

- failed login log yok
- suspicious API usage yok
- SIEM entegrasyonu yok


# Önleme

- Centralized logging

- Alert systems

- SIEM kullanımı

Örnek:

- Splunk
- ELK
- Wazuh


--- 


# 10. Mishandling of Exceptional Conditions


Beklenmeyen durumların:

- yanlış yönetilmesi,
- fail-open olması,
- sistem güvenliğini bozmasıdır.



Riskler;
- authentication bypass
- payment bypass
- privilege escalation

Önleme;

Fail-secure design

Hata varsa:
- Erişimi engelle

