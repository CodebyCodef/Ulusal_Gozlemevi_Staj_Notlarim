
Adımlar : 
1.  Kullanıcı Frontend üzerinden fotoğraf seçer
2.  FastAPI' ye  post isteği gönderir (sicil_no ile birlikte file)
3.  FastAPI fotoğrafı alır ve S3' upload eder
4.  S3 "response" döner --> Response = Fotoğraf URL
5.  Backend veritabanına sadece URL kaydeder.
6.  Frontend' e success response gönderilir.

Fotoğrafın sistem de okuma akışı

1.  Frontend Personel listesini ister ( /api/personeller)
2.  Backend veritabanından veriler + S3 URL lerini getirir
3.  Frontedn S3 URL sini kullanarak doğrudan fotoğrafı gösterir.