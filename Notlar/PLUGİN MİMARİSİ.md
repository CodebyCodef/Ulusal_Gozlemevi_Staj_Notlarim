# Plugin Mimarisi (Plugin Architecture)

## 1. Plugin Nedir?

Plugin (eklenti), mevcut bir yazılımın **çekirdek kodunu değiştirmeden**
yeni özellikler eklemeyi sağlayan modüler yazılım bileşenidir.

Temel amaç:

-   Uygulamayı genişletilebilir yapmak
-   Çekirdek sistemi sade tutmak
-   Üçüncü parti geliştiricilerin katkı yapabilmesini sağlamak

Plugin mimarisi genellikle şu prensibe dayanır:

> **Core sistem + eklentiler (plugins)**

Core sistem minimum işlevi sağlar, pluginler ise ek yetenekler
kazandırır.

------------------------------------------------------------------------

## 2. Plugin Mimarisi Nasıl Çalışır?

Plugin mimarisi genellikle şu bileşenlerden oluşur:

### 1. Core (Çekirdek Sistem)

Ana uygulamadır.

Sorumlulukları:

-   Pluginleri yüklemek
-   Plugin lifecycle yönetmek
-   Plugin API sunmak

### 2. Plugin Interface / Contract

Pluginlerin uygulaması gereken ortak arayüzdür.

Örnek:

``` python
class PluginInterface:
    def initialize(self):
        pass

    def execute(self):
        pass
```

Tüm pluginler bu interface'i implement eder.

------------------------------------------------------------------------

### 3. Plugin Loader

Pluginleri dinamik olarak yükleyen mekanizmadır.

Örneğin:

-   klasörden plugin tarama
-   DLL / shared library yükleme
-   Python module import

Basit Python örneği:

``` python
import importlib

plugin = importlib.import_module("plugins.example_plugin")
plugin.run()
```

------------------------------------------------------------------------

### 4. Plugin Lifecycle

Pluginlerin çalışma sürecindeki durumlarıdır.

Genellikle:

1.  Discover (plugin bulunur)
2.  Load (yüklenir)
3.  Initialize (başlatılır)
4.  Execute (çalışır)
5.  Shutdown (kapatılır)

------------------------------------------------------------------------

## 3. Plugin Mimarisinin Avantajları

### Modülerlik

Kod parçaları ayrıdır.

### Genişletilebilirlik

Yeni özellik eklemek için çekirdek kod değiştirilmez.

### Topluluk katkısı

Üçüncü parti geliştiriciler plugin yazabilir.

### Bakım kolaylığı

Plugin hatası çekirdek sistemi bozmaz.

------------------------------------------------------------------------

## 4. Plugin Mimarisinin Dezavantajları

### Versiyon uyumsuzluğu

Plugin API değişirse eski pluginler çalışmayabilir.

### Güvenlik

Üçüncü parti pluginler zararlı olabilir.

### Performans

Çok fazla plugin sistemi yavaşlatabilir.

------------------------------------------------------------------------

## 5. Plugin Mimarisi Kullanan Sistemler

### WordPress

WordPress'in gücünün büyük kısmı plugin ekosisteminden gelir.

Örnek:

-   SEO pluginleri
-   Cache pluginleri
-   Security pluginleri

------------------------------------------------------------------------

### VS Code

VS Code tamamen plugin temelli genişletilebilir bir editördür.

Örnek:

-   Python extension
-   Docker extension
-   GitLens

------------------------------------------------------------------------

### Web Tarayıcıları

-   Chrome Extensions
-   Firefox Add-ons

------------------------------------------------------------------------

## 6. Plugin Mimarisi Tasarım Desenleri

Plugin sistemleri genellikle şu design patternlerle birlikte kullanılır:

### Strategy Pattern

Davranışı runtime'da değiştirmek.

### Dependency Injection

Pluginlerin bağımlılıklarını yönetmek.

### Event Bus / Observer

Pluginlerin olaylara tepki vermesi.

### Service Locator

Plugin servislerini merkezi olarak bulmak.

------------------------------------------------------------------------

## 7. Basit Plugin Sistemi (Python Örneği)

Dizin yapısı:

    project
    │
    ├─ core
    │   └─ plugin_manager.py
    │
    ├─ plugins
    │   ├─ plugin_a.py
    │   └─ plugin_b.py
    │
    └─ main.py

Plugin Manager:

``` python
import importlib
import os

PLUGIN_FOLDER = "plugins"

def load_plugins():
    plugins = []
    for file in os.listdir(PLUGIN_FOLDER):
        if file.endswith(".py"):
            name = file[:-3]
            module = importlib.import_module(f"{PLUGIN_FOLDER}.{name}")
            plugins.append(module)
    return plugins
```

Main:

``` python
from core.plugin_manager import load_plugins

plugins = load_plugins()

for plugin in plugins:
    plugin.run()
```

Plugin:

``` python
def run():
    print("Plugin çalıştı")
```

------------------------------------------------------------------------

## 8. Plugin Sistemi Ne Zaman Kullanılır?

Aşağıdaki durumlarda tercih edilir:

-   Büyük ve genişletilebilir sistemlerde
-   Üçüncü parti geliştirici desteği isteniyorsa
-   Çok sayıda opsiyonel özellik varsa
-   SaaS veya platform ürünlerinde

Örnek:

-   IDE
-   CMS
-   Oyun motorları
-   Veri işleme platformları

------------------------------------------------------------------------

## 9. Özet

Plugin mimarisi:

-   Core sistemi küçük tutar
-   Özellikleri modüler hale getirir
-   Geniş bir ekosistem oluşturulmasını sağlar

Bu mimari özellikle **platform tabanlı yazılımlar** için kritik öneme
sahiptir.
