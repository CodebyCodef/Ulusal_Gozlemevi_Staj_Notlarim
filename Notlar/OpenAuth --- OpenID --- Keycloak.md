
# <span style = "color:lightblue"> OpenAuth </span>

OAuth bir **anahtar teslim etme** protokolüdür. Şifreni paylaşmadan, bir uygulamanın senin adına belirli kaynaklara (örneğin Google fotoğraflarına) erişmesine izin verir.

- **Odak noktası:** "Bu uygulama benim adıma ne yapabilir?"

ANA AMAÇ : Authorization yani yetkilendirme.



# <span style = "color:lightblue"> OpenID </span>

OAuth 2.0'ın üzerine inşa edilmiş bir katmandır. OAuth "ne yapabileceğini" söylerken, OIDC "kim olduğunu" söyler. Bir uygulamaya Google veya Facebook ile giriş yaptığında çalışan sistem budur.

- **Odak noktası:** "Bu kişi kim?"

ANA AMAÇ : Authentication yani kimlik doğrulama 


# <span style = "color:lightblue"> Keycloak </span>

Yukarıdaki protokolleri (OAuth, OIDC, SAML) uygulaman için hazır bir paket olarak sunan **açık kaynaklı bir yazılımdır.** Kendi kullanıcı veritabanını yönetmeni, sosyal girişleri (Login with Google vb.) entegre etmeni ve yetkilendirme kuralları koymanı sağlar.



![[OpenAuth - OpenID - Keycloak|| 500]]


![[OPENAUTH _ ONLY]]

![[KEYCLOAK _ ONLY]]