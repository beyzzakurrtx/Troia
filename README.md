# 📦 Parçaların Sevkiyat İçin Depoda Bekleme Süresini Otomatik Mail Atarak Raporlayan Sistem

## 📌 Proje Hakkında

Bu proje, üretim yapan ve ürünlerini stoklu çalışan firmalar için yaygın bir ihtiyaca çözüm sunar. Üretim sonucunda oluşan paketlenmiş ürünler, genellikle **SVK** gibi özel depolarda tutulur. Bu ürünler, sipariş geldikçe irsaliyelendirilerek sevk edilir. Ancak bazı ürünler uzun süre depoda bekleyebilir ve bu durum ürünün kalite standartlarını etkileyebilir (örneğin; deformasyon, bozulma, geçerliliğini yitirme, oksitlenme vb.).

Bu ihtiyaca yönelik olarak geliştirilen bu sistem sayesinde:
- Belirli bir süreden (örneğin 1 yıl) uzun süredir **SVK deposunda** bekleyen parçalar tespit edilir,
- Bu parçalara ait **malzeme kodu, parti numarası, son işlem tarihi** gibi bilgiler toplanır,
- HTML formatında tablo satırları oluşturularak otomatik bir e-posta içeriği hazırlanır,
- Kalite ve bilgi işlem gibi ilgili departmanlara otomatik e-posta gönderimi yapılır.

---

## ⚙️ Kullanılan Teknolojiler

- **TROIA  Dili** 
- SQL sorguları 
- Otomatik e-posta gönderimi için `SENDMAIL` komutu
- Dinamik HTML tablo satırları üretimi
- Canias ERP Destek Tabloları

---

## 🚀 Özellikler

- **SVK deposunda** bulunan ve:
  - Malzeme kodu 16 karakter olan,
  - Stok yeri `P` ile başlayan,
  - 1 yıldan fazla süredir hareket görmemiş olan,
  - Geçerli bir irsaliye ile çıkışı yapılmamış ürünler sistem tarafından tespit edilir.
- Ürünlere ait bilgiler, SQL sorguları aracılığıyla ilgili tablolardan çekilir.
- E-posta şablonunda `#TABLEROWS#` etiketi yerine dinamik olarak oluşturulmuş tablo satırları yerleştirilir.
- Mail, tanımlı kullanıcı adı, şifre, host ve TLS protokolü kullanılarak güvenli şekilde gönderilir(Canias içerisindeki destek tablosuna girilen veilerden alınır.).

---

## 📧 Otomatik Gönderilen E-Posta İçeriği

| Malzeme Kodu | Çizim No / Malzeme | Parti No | Son İşlem Tarihi |
|--------------|--------------------|----------|-------------------|
| 1234567890123456 | DRAW-001           | B12345   | 15.04.2023        |
| ...          | ...                | ...      | ...               |

Bu yapı sayesinde kalite güvence ekipleri, deforme olabilecek ürünler için erken aksiyon alabilir.

---

## 🛠 Kurulum ve Kullanım

Bu sistem, **Canias ERP** üzerinde çalışacak şekilde yazılmıştır. Kurulum için:
1. Oluşturulan bir dialogun SYST00 ekranından Dialogun Toplu İşlemler alanında bu fonksiyon çalıştırılır.
-*-*-*
THIS.STOCKWAITINFORM();
SHUTDOWN;
-*-*-*
2. Gönderim yapılacak adresleri ve şablon metnini `IASCLB011` ve `IASBPM012` tablolarında tanımlayın. (Destek Tabloları)
3. Otomatik çalıştırılması için sistemde bir BATCH tanımı yapılabilir, bu işlem zamanlanmış bir görev (JOB) ile veya manuel olarak çalıştırılabilir.

---

## 👩‍💼 Kullanım Senaryosu

> “SVK deposunda bekleyen parçaların bir süredir hareket görmediğini ve kalite riski taşıyabileceğini fark ettik. Artık sistemimiz bu parçaları otomatik olarak tespit edip, ilgili kişilere raporlayarak zamanında müdahale imkanı sağlıyor.”

---

