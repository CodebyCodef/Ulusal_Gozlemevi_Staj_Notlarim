
# 📦 ABC Kütüphaneleri (Abstract Base Classes) — Detaylı Rehber

Python’da **ABC (Abstract Base Classes)**, belirli bir yapıyı zorunlu kılmak ve kod standartlarını korumak için kullanılan güçlü bir araçtır. Özellikle büyük projelerde veya ekip çalışmalarında **tutarlı mimari** oluşturmak için kritik öneme sahiptir.

---

## 🧠 ABC Nedir?

ABC, yani _Abstract Base Class_, diğer sınıflar için bir **şablon (template)** görevi görür.

Bu sınıflar:

- Doğrudan kullanılamaz (instance oluşturulamaz)
    
- Alt sınıfların belirli metodları implement etmesini zorunlu kılar
    

---

## 🎯 Neden ABC Kullanılır?

ABC kullanmanın temel amaçları:

- Kod standartlarını zorunlu hale getirmek
    
- Hataları daha erken yakalamak
    
- Büyük sistemlerde düzen sağlamak
    
- Interface benzeri yapı kurmak
    

---

## ⚙️ Python'da ABC Kullanımı

Python’da ABC kullanmak için `abc` modülü kullanılır.

### Temel kullanım:

```python
from abc import ABC, abstractmethod

class Animal(ABC):

    @abstractmethod
    def speak(self):
        pass
```

Bu noktada:

- `Animal` sınıfı artık soyut (abstract) bir sınıftır
    
- `speak()` metodu implement edilmek zorundadır
    

---

## ❗ Önemli Kural

Eğer bir sınıf, abstract methodları implement etmezse:

```python
class Dog(Animal):
    pass

dog = Dog()  # ❌ HATA verir
```

Hata alırsın çünkü `speak()` implement edilmedi.

---

## ✅ Doğru Kullanım

```python
class Dog(Animal):
    
    def speak(self):
        return "Hav hav"

dog = Dog()
print(dog.speak())
```

---

## 🧱 ABC'nin Sağladığı Yapısal Avantaj

ABC aslında şu problemi çözer:

> "Bu sınıfı kullanan herkes aynı metodları yazmak zorunda olsun"

Bu sayede:

- API tutarlılığı sağlanır
    
- Kod okunabilirliği artar
    
- Büyük sistemler daha yönetilebilir olur
    

---

## 🔄 Gerçek Hayat Senaryosu

Bir ödeme sistemi düşün:

```python
class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
```

Farklı ödeme yöntemleri:

```python
class CreditCardPayment(Payment):
    def pay(self, amount):
        print(f"Kredi kartı ile {amount} ödendi")

class PayPalPayment(Payment):
    def pay(self, amount):
        print(f"PayPal ile {amount} ödendi")
```

Burada garanti edilen şey:  
👉 Her ödeme sınıfı `pay()` metoduna sahip olmak zorunda

---

## 🔍 ABC vs Normal Class

|Özellik|Normal Class|ABC|
|---|---|---|
|Instance oluşturma|✅|❌ (direct)|
|Metod zorunluluğu|❌|✅|
|Mimari kontrol|❌|✅|

---

## 🧩 Interface Mantığı (Java ile Kıyas)

ABC, Java’daki `interface` yapısına benzer:

- Metod tanımlarsın
    
- İçeriğini alt sınıflar doldurur
    

Ama Python daha esnek:

- İstersen hem abstract hem concrete metod yazabilirsin
    

---

## 🚀 Ne Zaman Kullanmalısın?

ABC kullanmak mantıklıdır eğer:

- Birden fazla benzer sınıfın varsa
    
- Hepsinin aynı metodları implement etmesini istiyorsan
    
- Framework benzeri yapı kuruyorsan
    

---

## 🧪 Ekstra: Abstract Property

Sadece metod değil, property de zorunlu yapılabilir:

```python
from abc import ABC, abstractmethod

class Shape(ABC):

    @property
    @abstractmethod
    def area(self):
        pass
```

---

## 🧪 Ekstra: Default (Concrete) Metod

ABC içinde normal metod da yazabilirsin:

```python
class Animal(ABC):

    @abstractmethod
    def speak(self):
        pass

    def info(self):
        print("Ben bir hayvanım")
```

---

## 🧭 Best Practice Önerileri

- ABC’yi **interface gibi düşün**
    
- Method isimlerini iyi seç (contract önemli)
    
- Gereksiz soyutlama yapma
    
- Küçükten başla, ihtiyaç oldukça ekle
    

---
