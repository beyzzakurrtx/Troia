✉️ Troia – Otomatik E-Posta Gönderim Fonksiyonu
Bu kod parçası, Canias ERP üzerinde TROIA dili kullanılarak geliştirilmiş, sistemde kayıtlı kullanıcı bilgileri ve önceden tanımlanmış şablonlar kullanılarak otomatik HTML formatında e-posta 
gönderimi yapan fonksiyondur.

📬 Fonksiyonun Amacı
Belirlenen kullanıcı ve SMTP sunucu bilgileri ile dinamik içerikli e-posta oluşturmak ve göndermek.

Test ve canlı ortamları ayırarak hatalı mail gönderimlerinin önüne geçmek.

Kullanıcıya zamanında ve kişiselleştirilmiş bilgilendirme sağlamak.

⚙️ Çalışma Prensibi
SMTP Sunucu Bilgilerinin Çekilmesi
IASCLB011 tablosundan gönderici mail adresine ve SMTP bağlantı parametrelerine (host, kullanıcı adı, parola) erişilir.
Bu Canias ERP de destek tablolarında tanımlanır.

Mail İçeriğinin Şablondan Oluşturulması
IASBPM012 tablosundaki dil ve şirket bazlı mail metni çekilir.
İçerikteki yer tutucular (#CLKUSER#, #CLKUSERPASS# vb.) ilgili değişkenlerle dinamik olarak değiştirilir.
E-posta HTML formatına çevrilir. 
--HTML kodu ektedir.

*** Önizleme Ekran Görüntüsü:

![sendmaıl1](https://github.com/user-attachments/assets/cd2a3b8b-7e3a-48eb-8264-6e50ae9e2a11)

Alıcıların Belirlenmesi
Kullanılan veritabanı adı alınır (GETUSERINFO('database_name')).
Test ortamında mail adresleri boş bırakılırken, canlı ortamda gerçek alıcı adresleri atanır.
Amaç: Test ortamında çalışmasın, sadece canlı ortamda çalışsın.

Mail Gönderimi
SENDMAIL fonksiyonu kullanılarak mail gönderilir.
SMTP sunucu bilgileri, kullanıcı adı, parola ve alıcı adresleri parametre olarak iletilir.
İletişim TLS protokolü ile şifrelenir.

İşlemin Sonlandırılması
Gönderim tamamlandıktan sonra işlem SHUTDOWN; komutu ile sonlandırılır.

💡 Kullanım Alanları
Sistem kullanıcılarına otomatik bilgilendirme e-postaları göndermek.

İş akış süreçlerinde bildirim ve onay mail’leri oluşturmak.

Dinamik ve şablon tabanlı e-posta içerikleriyle kullanıcı deneyimini artırmak.

📌 Teknik Notlar
SMTP bilgileri veritabanından çekildiği için güncelleme gereksinimi kolay yönetilir.

Şablon metinlerdeki değişkenler kolayca genişletilebilir veya değiştirilebilir.

Test ve canlı ortam ayrımı ile güvenlik ve hata önleme sağlanır.

👩‍💻 Geliştirici Notu
Bu işlem, Canias kullanıcılarının ihtiyacı doğrultusunda istenilen veriler sağlanarak otomatik mail gönderilmesi için yapılmıştır.
