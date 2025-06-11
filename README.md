
# 🔧 Troia – Fire Oranları Raporu

Bu proje, **Canias ERP** üzerinde **TROIA** dili kullanılarak geliştirilmiş bir rapor ekranıdır.  
Amaç, üretim sürecinde çeşitli noktalarda oluşan **firelerin** fire tipine göre **fire oranlarını** ve ilgili üretim bilgilerini detaylı bir şekilde raporlamaktır.

---

## 📊 Rapor İçeriği

Rapor aşağıdaki bilgileri hesaplar ve kullanıcıya sunar:

- Fire tipi (`REWORKKEY`) bazlı gruplanmış veri
- Her fire tipi için:
  - Fire miktarı
  - Onaylanmış üretim miktarı
  - Fire oranı (yüzde)
- Genel fire oranı (toplam bazda)
- Görsel ayrıştırma: Fire tipi bazlı ara toplam satırları **sarı arka plan** ile vurgulanır
- Her satır için toplam içerisindeki fire yüzdesi

---

## ⚙️ Kullanılan Teknolojiler

- Canias ERP (TROIA dili)
- Dahili değişken ve tablo işlemleri
- Renkli satır ayırma (highlighting)
- Veri toplama ve oran hesaplama algoritmaları

---

## 🖼️ Ekran Görüntüsü

Aşağıda rapor ekranının örnek görünümü yer almaktadır:

![reworkreport1](https://github.com/user-attachments/assets/ca08d97a-e32e-4f25-8e1a-d14c5e8821ac)

---

## 📌 Teknik Notlar

- Kodda geçici tablo olarak `REPORTTABLETMP`, rapor tablosu olarak `REPORTTABLE` kullanılmaktadır.
- `LOOP` ve `LOCATERECORD` yapıları ile veriler filtrelenip gruplanır.
- `SETBACKCOLOR TO YELLOW` komutu ile sarı ara toplam satırları eklenir.
- Toplam hesapları `TOTALR`, `TOTALRO`, `SUMREWORKRATE` gibi değişkenler ile yönetilir.

---

## 👩‍💻 Geliştirici Notu

Bu rapor, Canias kullanıcılarının fire analizlerini daha etkin ve görsel olarak takip edebilmelerini sağlamak amacıyla geliştirilmiştir.

---
