## 📌 Tanım

Composite Design Pattern, nesneleri ağaç yapısı şeklinde organize ederek tekil nesneler ile nesne gruplarını aynı arayüz üzerinden yönetmeyi sağlar.

---

## 🎯 Amaç

- Tekil ve çoğul nesneleri aynı şekilde kullanmak
    
- Karmaşık hiyerarşik yapıları basitleştirmek
    

---

## 🧱 Yapı

### 1. Component

Tüm nesneler için ortak arayüz.

### 2. Leaf

Alt elemanı olmayan nesneler.

### 3. Composite

Alt nesneleri içeren yapılar.

---

## 🌳 Yapı Şeması

```
Component
   ├── Leaf
   └── Composite
         ├── Leaf
         └── Leaf
```

![[Pasted image 20260422100547.png|| 500]]

![[Excalidraw/Composite Design Pattern || 900]]

---

## 🧪 Python Örneği

```python
from abc import ABC, abstractmethod

class Component(ABC):
    @abstractmethod
    def operation(self):
        pass

class Leaf(Component):
    def operation(self):
        print("Leaf node")

class Composite(Component):
    def __init__(self):
        self.children = []

    def add(self, component):
        self.children.append(component)

    def operation(self):
        print("Composite node")
        for child in self.children:
            child.operation()
```

---

## ⚖️ Avantajlar

- Tek tip kullanım sağlar
    
- Hiyerarşik yapı yönetimi kolay
    
- Genişletilebilir
    

---

## ⚠️ Dezavantajlar

- Karmaşıklık artabilir
    
- Tip kontrolü zorlaşır
    

---

## 🧠 Kullanım Alanları

- Dosya sistemleri
    
- UI bileşenleri
    
- Organizasyon yapıları
    
- Menü sistemleri
    

---

## 📎 Özet

Composite Pattern, özellikle ağaç yapıları ile çalışırken büyük kolaylık sağlar ve kodun daha esnek olmasına yardımcı olur.