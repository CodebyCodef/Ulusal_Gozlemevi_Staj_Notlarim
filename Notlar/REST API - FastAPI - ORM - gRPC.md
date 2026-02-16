	

# REST API mantığı

- ## Resources Kavramı
	- API '  de her şey bir kaynaktır
	- ÖRN:
		- /users
		- /products
		- /orders


- ## HTTP Method

	- GET  :  Veri getir
	- POST :  Yeni veri oluştur
	- PUT :  Veriyi tamamen güncelle
	- PATH :  Kısmi güncelle
	- DELETE :  Sil


*Sınucu, her isteği bağımsız değerlendirir. Yani istek içinde gerekli tüm bilgiler bulunmalıdır*



![[working_of_an_api_6cc55c5cd1.webp ]]


## Asla Expose Edilmemesi Gereken Fieldlar


- IsAdmin
- Role
- PasswordHash
- CreatedAt
- UpdatedAt
- IsDeleted
- OwnerUserId
- InternalFlags

---

### DTO Nedir? 
Açılımı __Data Transfer Object__ (Türkçeye __Veri Transfer Nesnesi__ olarak çevrilmiştir) dir. Temel amacı veriyi veri tabanından alıp, , istemciye gönderirken sadece gerekli olan kısmı paketlemektir.

#### DTO Kullanımı

- Güvenlik (Security) :  Hassas verileri gizleme
-  Performans (Performance) : Kullanıcının ihtiyacı olmayan  verileri göndermeyerek ağ ağ trafiğini azaltırsın.
-  Bağımsızlık  (Decoumpling) : Veritabanı tablonda değişiklik yapsan bile  DTO sayesinde APİ yi kullanan tarafları bozmadan aradaki eşleştirmeyi düzeltebilirsin.

```csharp
public class User {
    public int Id { get; set; }
    public string Username { get; set; }
    public string PasswordHash { get; set; } // GİZLİ KALMALI
    public bool IsAdmin { get; set; } // GİZLİ KALMALI
    public bool IsDeleted { get; set; } // GEREKSİZ
}
```
- Veritabanı tablosu

```csharp
public class UserDTO {
    public string Username { get; set; }
    // Sadece kullanıcı adını gönderiyoruz, şifre ve yetkiler gizlendi.
}
```
- API yanıtı olarak dönecek DTO


**Özetle DTO; veritabanındaki "ham" veriyi, sunum katmanına uygun "işlenmiş/filtrelenmiş" veriye dönüştüren bir kap (container) görevi görür. İçinde asla iş mantığı (metotlar, hesaplamalar) bulunmaz, sadece özellikler (properties) bulunur.**


---
---
---

# FAST API Hakkında


FastAPI = Python tabanlı, async destekli, modern bir web API frameworküdür.

- En basit şekilde FastApi örneği:
```python 
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"message": "API çalışıyor"}
```



-  FastApi ve .Net arasında ki benzerlikler

| ASP.NET Core  | FastAPI            |
| ------------- | ------------------ |
| Controller    | @app decorator     |
| Model         | Pydantic BaseModel |
| Validation    | Pydantic otomatik  |
| IActionResult | JSON dict          |
| NotFound()    | HTTPException      |
| Swagger       | /docs              |

## BaseModel 

1. Request body’yi parse eder
    
2. Tip kontrolü yapar
    
3. Otomatik validation yapar
    
4. JSON → Python objesi dönüşümü yapar
    
5. Swagger şeması üretir


# SQLalchemy - Pydantic ilişki şeması

![[SQLalchemy-Pydantic Şeması| Pydantic - SQLalchemy çalışma mantığı|6000]]


## Basit Şekilde SQLalchemy - SQLlite Engine


```python
from sqlalchemy import create_engine  
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

SQLALCHEMY_DATABASE_URL = "sqlite:///./sql_app.db"

engine = create_engine(

    SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False}
)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()
```


# SQLalchemy örnek model sınıfı

```python 
from sqlalchemy import Column, Integer, String, Boolean, Float
from databaseEngine import Base
  
class Urun(Base):
    __tablename__ = "urunler"

    id = Column(Integer, primary_key=True, index=True)
	ad = Column(String, index=True)
    fiyat = Column(Float)
    stokta = Column(Boolean, default=True)
```


# Örnek Senaryo (ürün oluşturma , kaydetme, listeleme)


```python
from fastapi import FastAPI, Depends, HTTPException
from sqlalchemy.orm import Session
from typing import List
from pydantic import BaseModel
  
import database as models
import databaseEngine as engine

  
models.Base.metadata.create_all(bind=engine.engine)
    
app = FastAPI()

  

def get_db():
    db = engine.SessionLocal()
    try:
        yield db
    finally:
        db.close()

class UrunBase(BaseModel):
    id: int
	ad: str
    fiyat: float
    stok: bool = True
  
# Buradaki "pass" ifadesi, UrunCreate sınıfının UrunBase sınıfından türetildiğini ve
#  şu anda ek bir özellik veya davranış içermediğini belirtir.
# Bu, gelecekte UrunCreate sınıfına
# özel özellikler eklemek istediğinizde kolayca genişletilebilir hale getirir.
  
#kısaca inheritance diyebiliriz.
class UrunCreate(UrunBase):
    pass
     
class Urun(UrunBase):
    id:int
    class Config:
        orm_mode = True


@app.post("/api/urunler", response_model=Urun)

def urun_ekle(urun: UrunCreate, db: Session = Depends(get_db)):

    db_urun = models.Urun(ad=urun.ad, fiyat=urun.fiyat, stokta=urun.stok)
    db.add(db_urun)
    db.commit()
    db.refresh(db_urun)

    return db_urun


@app.get("/api/urunler/", response_model=List[Urun])
def urunleri_listele(skip: int = 0, limit: int = 100, db: Session = Depends(get_db)):

    urunler = db.query(models.Urun).offset(skip).limit(limit).all(
    return urunler

  

@app.get("/api/urunler/{urun_id}", response_model=Urun)
def urun_getir(urun_id : int, db: Session = Depends(get_db)):

    db_urun = db.query(models.Urun).filter(models.Urun.id == urun_id).first()
    if db_urun is None:
        raise HTTPException(status_code=404, detail="Ürün bulunamadı")

    return db_urun
    
```




--- 


# gRPC işlemlerine adım adım


![[proto-gRPC mimarisine bir göz atış|700]]


## ".proto " nedir?


- proto uzantılı dosya bizim __Sözleşmemiz (Contract)__ diyebiliriz. 




| **Özellik**      | **FastAPI (REST) 🐍** | **gRPC (Protobuf) 📜**     |
| ---------------- | --------------------- | -------------------------- |
| **Veri Tanımı**  | `Pydantic Model`      | `message`                  |
| **Veri Tipleri** | `str`, `int`, `float` | `string`, `int32`, `float` |
| **Alanlar**      | `ad: str`             | `string ad = 1;`           |