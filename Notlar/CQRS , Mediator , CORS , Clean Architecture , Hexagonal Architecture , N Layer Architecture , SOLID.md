---
aliases:
  - arch
  - solid
  - clean
tags:
  - "#architecture"
---
---


# <span style="color:lightblue"> CQRS</span>

#### (Command Query Responsibility Segregation)

##### Core : 

**Command :** Veriyi değiştirir (Update, Delete, Create). Geriye genellikle sadece işlem sonucu döner.

**Query :** Veriyi okur. Veri üzerinde asla değişiklik yapmaz. 

**Neden Kullanılır?** Bir haber sitesinde 1 kişi yorum yaparken 10.000 kişi haber okuyor olabilir. Okuma ve yazma yolları birbirinden ayrılırsa tarafsız olarak performans artışı sağlanabilir.


# <span style="color:lightblue"> Mediator</span>

##### Core :
Nesneler arasındaki karmaşık bağları koparıp, tüm iletişimi tek bir merkezden yönetmektir.

- Uçakların birbirleriyle telsizle konuşması yerine, hepsinin kuleyle konuşması gibi



# <span style="color:lightblue"> CORS</span>

#### Cross - Origin Resource Sharing

##### Core : 
Bir web sitesinin, kendi sunucusu dışındaki bir kaynaktan veri isteyip istemeyeceğine karar veren bir güvenlik mekanizmasıdır.

- Tarayıcı güvenliği protokolüdür. "Sen bu sitedeki veriye neden erişiyorsun"


---

# <span style="color:lightblue"> N-Tier (Katmanlı) Mimari</span>

##### Core :
Veriyi katmanlar üzerinden yukarıdan aşağıya taşımaktır. 
- Geleneksel. Her katman bir altındakine bağımlı.
- Küçük projeler için ideal , büyük ölçekli projeler için uygun <span style="color:red" > DEĞİL </span>



# <span style="color:lightblue"> Clean & Hexagonal Architecture </span>

<span style="color:rgb(230,80,85)" > !!! İş Mantığını (Domain) her şeyin merkezine koyar </span>

##### Hexagonal (Ports & Adapters) : 
Uygulamanın dış dünya ile iletişimini "Port"lar aracılığıyla yapar. Dışarıdaki her şey birer "Adaptör"dür.

##### Clean Architecture : 
EN İÇTE **Entities** ve **Use Cases** vardır. Veritabanı ve Frameworkler EN DIŞ halkadadır.

##### nOT : Bağımlılıklar her zaman içeriye doğrudur. İç katmani dışarıda ne olup bittiğini bilmez.

----
