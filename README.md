📘 PARSE Komutunun Genel Yapısı:

PARSE <ANA_STRING> INTO <HEDEF_DEĞİŞKEN> DELIMITER <AYRAÇ>
BEGIN
    // Her parça için çalışacak işlemler
ENDPARSE;


🔍 Açıklaması:
ANA_STRING: Ayırmak istediğiniz tam metin.

INTO <HEDEF_DEĞİŞKEN>: Her ayrılmış parçanın atanacağı değişken.

DELIMITER: Ayırıcı karakter (örn: '|', ',', ';' vs.)

BEGIN ... ENDPARSE: Her parça için yapılacak işlemler bu blok içinde yazılır.

➡️ Örnek:

OBJECT:
    STRING PARCALAR, TOKEN;

PARCALAR = 'Ali,Ayşe,Mehmet,Can';
PARSE PARCALAR INTO TOKEN DELIMITER ','
BEGIN
    MESSAGE TOKEN;
ENDPARSE;

↘️ Çıktı:

Ali
Ayşe
Mehmet
Can

⚠️ Notlar:
Her TOKEN bir döngü turunda parçalanmış bir değeri tutar.

CONTINUE komutu ile o parçayı atlayabilirsiniz.

Sayı kontrolü için ISNUMERIC(TOKEN) gibi fonksiyonlarla kombin edilebilir.

-- Örneğin :

OBJECT:
        STRINGBUILDER SB,
        STRING STRNEWLINE,
        STRING MAINSTRING,
        STRING TOKEN;
SB = '';
STRNEWLINE = TOCHAR(10);
MAINSTRING = '1|A|2|B|3|C|4|D|5|E';
PARSE MAINSTRING INTO TOKEN DELIMITER '|'
BEGIN
IF !ISNUMERIC(TOKEN) THEN
                CONTINUE;
        ENDIF;
APPENDSTRING TOKEN TO SB;
        APPENDSTRING ' is a number.' TO SB;
        APPENDSTRING STRNEWLINE TO SB;
ENDPARSE;

->>>> Çıktı
  1 is a number. 
  2 is a number. 
  3 is a number. 
  4 is a number.
  5 is a number.

