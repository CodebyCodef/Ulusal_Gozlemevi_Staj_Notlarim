# 🚀 Factory Design Pattern

> Nesne üretimini kontrol altına al, bağımlılıkları azalt, kodunu ölçeklenebilir hale getir.

---

## 📌 Nedir?

Factory Design Pattern (Fabrika Tasarım Deseni), nesne oluşturma sürecini merkezileştirerek istemcinin (client) hangi sınıfın örneğini oluşturduğunu bilmesini gereksiz hâle getiren bir **creational (oluşturucu) design pattern**'dır.

### 🎯 Amaç

- Nesne oluşturmayı soyutlamak
- Kod bağımlılığını azaltmak (*loose coupling*)
- Yeni türler eklemeyi kolaylaştırmak (*Open/Closed Principle*)

---

## 🧠 Ne Zaman Kullanılır?

- Aynı interface'i implement eden birden fazla sınıf varsa
- Hangi nesnenin oluşturulacağı runtime'da belirleniyorsa
- Kodda doğrudan `new` kullanımını azaltmak istiyorsan

---

## 🏗️ Yapısı

Factory Pattern genellikle 3 ana bileşenden oluşur:

1. **Product (Ürün)** → Ortak interface
2. **Concrete Product (Somut Ürünler)** → Interface'i implement eden sınıflar
3. **Factory (Fabrika)** → Nesne oluşturma sorumluluğunu üstlenen yapı

---

## 🔧 Örnek Senaryo

Bir **Notification sistemi** düşün:

- Email
- SMS
- Push Notification

---

## ❌ Factory Kullanmadan

```python
class EmailNotification:
    def send(self):
        print("Email gönderildi")

class SMSNotification:
    def send(self):
        print("SMS gönderildi")

# Kullanım
notif = EmailNotification()
notif.send()
```

### ⚠️ Problem

- Client doğrudan somut sınıfa bağımlıdır
- Yeni tür eklemek mevcut kodu değiştirmeyi gerektirir

---

## ✅ Factory Pattern ile

### 1. Product (Interface)

```python
from abc import ABC, abstractmethod

class Notification(ABC):
    @abstractmethod
    def send(self):
        pass
```

---

### 2. Concrete Products

```python
class EmailNotification(Notification):
    def send(self):
        print("Email gönderildi")

class SMSNotification(Notification):
    def send(self):
        print("SMS gönderildi")

class PushNotification(Notification):
    def send(self):
        print("Push bildirimi gönderildi")
```

---

### 3. Factory Class

```python
class NotificationFactory:
    @staticmethod
    def create_notification(notification_type):
        if notification_type == "email":
            return EmailNotification()
        elif notification_type == "sms":
            return SMSNotification()
        elif notification_type == "push":
            return PushNotification()
        else:
            raise ValueError("Geçersiz notification type")
```

---

### 4. Kullanım

```python
notif = NotificationFactory.create_notification("sms")
notif.send()
```

---

## 🔥 Avantajları

- ✅ Loose coupling sağlar
- ✅ Kod okunabilirliğini artırır
- ✅ Yeni sınıf eklemek kolaydır
- ✅ Single Responsibility Principle ile uyumludur

---

## ⚠️ Dezavantajları

- ❌ Kod karmaşıklığı artabilir
- ❌ Küçük projelerde gereksiz olabilir

---

## 💡 Gerçek Hayat Analojisi

Bir **restoran** düşün:

- Sen sadece "pizza" söylersin
- Nasıl yapıldığıyla ilgilenmezsin

👉 Burada:

- Sen = Client
- Restoran = Factory
- Pizza = Product

---

## 🧩 Bonus: Daha Gelişmiş Versiyon (Dictionary ile)

```python
class NotificationFactory:
    _creators = {
        "email": EmailNotification,
        "sms": SMSNotification,
        "push": PushNotification
    }

    @classmethod
    def create_notification(cls, notification_type):
        if notification_type not in cls._creators:
            raise ValueError("Geçersiz tür")
        return cls._creators[notification_type]()
```

---

## 🧪 Test Örneği

```python
def test_notification():
    types = ["email", "sms", "push"]
    for t in types:
        notif = NotificationFactory.create_notification(t)
        notif.send()

if __name__ == "__main__":
    test_notification()
```

---

## 📚 Özet

Factory Pattern:

- Nesne oluşturmayı merkezi hâle getirir
- Client'ı somut sınıflardan ayırır
- Genişletilebilir ve sürdürülebilir bir yapı sağlar

---

## 🏁 Son Not

Bu doküman son bir gözden geçirmeden geçirilmiş, dil bilgisi ve anlatım açısından iyileştirilmiştir. Artık doğrudan profesyonel bir README olarak kullanılabilir.

