
# 🔧 Troiada Tablolar Üzerinde Çalışma ve Tablo Manipülasyon Komutları 

TANIMLAMA:

     OBJECT:
     TABLE TMPTABLE;

     
STUN EKLEME:

  	APPEND COLUMN {columnname}, {columntype}, {columnlength} TO {table};
	  /* add a 100 char length string column named COL1 to TABLEVAR */
    APPEND COLUMN COL1, STRING, 100 TO TABLEVAR;
    APPEND COLUMN COL2, INTEGER, 10 TO TABLEVAR;
	  /* now table is able to store data */
	
! SELECT İLE STUN EKLEME:

    OBJECT:
        TABLE T1;
    /* change column-model and data of an existing variable */
    SELECT USERNAME, CREATEDBY, CREATEDAT FROM IASUSERS WHERE 1 = 2 INTO T1;
    /* define a table variable with its column-model */
    SELECT USERNAME, CREATEDBY, CREATEDAT FROM IASUSERS WHERE 1 = 2 INTO T2;

-- APPEND ROW
Bir tablo değişkenine programlı olarak yeni bir satır eklemek için APPEND ROW komutu kullanılır. Bu komut, yeni bir satırı ilk satıra, tablonun sonuna veya belirli bir satırın sonrasına ekleyebilir.

• APPEND ROW TO {table}; komutu, tabloya yeni bir satır ekler. Bu satır genellikle tablonun en sonuna eklenir.
• ATHEAD seçeneği, yeni satırın tablonun başına eklenmesini sağlar.
• ATBETWEEN seçeneği, yeni satırın mevcut bir satırdan sonra eklenmesini sağlar. Bu kullanımda, genellikle hedef satır belirtilmelidir (örneğin, satır numarası veya belirli bir koşul üzerinden eklenebilir).

    
    APPEND ROW TO {table} [ATHEAD | ATBETWEEN];
    OBJECT:
            TABLE T1;
    SELECT USERNAME, CREATEDBY, CREATEDAT FROM IASUSERS WHERE 1 = 2 INTO T1;
    APPEND ROW TO T1;

--ROW INDEX 
!!! Satır Indexleri 1 den başlar.

    OBJECT:
            TABLE T1,
            INTEGER ROWINDEX,
            STRING RESULT;
    ROWINDEX = 1;
    RESULT = '';
    SELECT USERNAME, CREATEDBY, CREATEDAT FROM IASUSERS INTO T1;
    WHILE ROWINDEX < T1_ROWCOUNT                    /*T1 tablosundaki toplam satır sayısı*/
    BEGIN
            RESULT = RESULT + T1[ROWINDEX]_USERNAME + ' created by ';
            RESULT = RESULT + T1[ROWINDEX]_CREATEDBY + ' at ';
            RESULT = RESULT + T1[ROWINDEX]_CREATEDAT + TOCHAR(10);
            ROWINDEX = ROWINDEX + 1;
    ENDWHILE;


 --ACTIVEROW: üzerinde işlem yapılan veya veriye erişilen şu anda "aktif" olan satırdır.
 
"Active Row" (Aktif Satır) ile "Selected Row" (Seçili Satır) aynı şey değildir

    OBJECT:
            TABLE T1,
            INTEGER ROWINDEX,
            STRING RESULT;
    ROWINDEX = 1;
    RESULT = '';
    SELECT USERNAME, CREATEDBY, CREATEDAT
            FROM IASUSERS
            INTO T1;
    WHILE ROWINDEX < T1_ROWCOUNT
    BEGIN
            T1_ACTIVEROW = ROWINDEX;
            RESULT = RESULT + T1_USERNAME + ' created by ';
            RESULT = RESULT + T1_CREATEDBY + ' at ';
            RESULT = RESULT + T1_CREATEDAT + TOCHAR(10);
            ROWINDEX = ROWINDEX + 1;
    ENDWHILE;


-AKTİF SATIRI OKUMAK

/* to a given index */
READ {table} WITH INDEX {activerowindex};
/* to an index related with current */
READ {table} WITH FIRST | LAST | NEXT | PREV;

• FIRST: İlk satırı aktif satır olarak ayarlar.
• LAST: Son satırı aktif satır olarak ayarlar.
• NEXT: Şu anki aktif satırdan bir sonraki satıra geçer ve onu aktif yapar.
• PREV: Şu anki aktif satırdan bir önceki satıra geçer ve onu aktif yapar.


ACTIVEROW (INTEGER, NO)
	• Açıklama: Bu bayrak, aktif satırın indeksini döndürür. İndeks, 1'den satır sayısına kadar olan bir değerdir. Yani, hangi satırın aktif olduğunu gösterir.
ROWCOUNT (INTEGER, YES)
	• Açıklama: Bu bayrak, tablodaki toplam satır sayısını döndürür.
DBTABLENAME (STRING, YES)
	• Açıklama: Bu bayrak, bir tablonun verilerini sağlayan veritabanı tablosunun adını döndürür. Bu, genellikle veri kaynağı tablosunun adını belirtir.
HASSELECTEDROW (INTEGER, YES)
	• Açıklama: Bu bayrak, belirtilen tablonun seçili bir satıra sahip olup olmadığını döndürür. Eğer tablonun seçili bir satırı varsa, 1 döner, aksi takdirde 0 döner.
ACTIVECOL (INTEGER, YES)
	• Açıklama: Bu bayrak, UI tablosu (kullanıcı arayüzü tablosu) içindeki aktif sütunun indeksini döndürür. Aktif sütun, kullanıcı tarafından seçilen veya üzerinde işlem yapılan sütundur.
ACTIVECOLNAME (STRING, YES)
	• Açıklama: Bu bayrak, UI tablosu içindeki aktif sütunun adını döndürür. Bu, aktif olan sütunun ismini sağlar.
ARROWSTATE (INTEGER, YES)
	• Açıklama: Bu bayrak, ArrowClick Event (Ok Tıklama Olayı) için bir durumu döndürür. Kullanıcı, tablodaki ok işaretine tıkladığında, bu durum aktif hale gelir ve ok işaretinin hangi durumda olduğunu gösterir.

SELECTED (INTEGER)
	• Açıklama: Bu bayrak, kullanıcı bir satırı seçtiğinde 1 değerini alır, aksi takdirde 0 olur.
HIDE (INTEGER)
	• Açıklama: Eğer bu bayrak 1 olarak ayarlanırsa, satır UI tablosunda görünmez hale gelir.
BKCOLOR (INTEGER)
	• Açıklama: Bu bayrak, satırın UI tablosundaki rengini değiştirmek için kullanılır. Genellikle, satırın arka plan rengini değiştirmek için kullanılır.
ROWTOOLTIP (STRING) / FYI
	• Açıklama: Bu bayrak, kullanıcı fareyi bir satır üzerinde durduğunda görünen tooltip (bilgi balonu) metnini belirler.
FILTERED (INTEGER)
	• Açıklama: Eğer satır bir UI filtresi nedeniyle görünmüyorsa, bu bayrak 1 olarak ayarlanır. Bu, kullanıcı arayüzünde tablonun filtrelenmesi sonucu bazı satırların gizlendiği durumları işaret eder.
SUMMARYROW (INTEGER)
	• Açıklama: Bu bayrak, toplamlar veya özet satırları için 1 olarak ayarlanmalıdır. Bu, toplam satırlarının hesaplama hatalarını önlemek için kullanılır.
CHECKED (INTEGER)
	• Açıklama: Bu bayrak, yalnızca TROIA uygulamaları tarafından ayarlanabilir ve okunabilir. Genellikle, satırın seçili olup olmadığını izlemek için kullanılır, ancak bu bayrak üzerinde dış müdahale yapılması önerilmez.

DELETED
	• Açıklama: Bu bayrak, bir satırın kullanıcı veya programcı tarafından silinip silinmediğini gösterir. Eğer satır silindiyse, DELETED bayrağı 1 olarak ayarlanır. Aksi takdirde 0 olur.
INSERTED
	• Açıklama: Bu bayrak, bir satırın yeni bir satır olup olmadığını gösterir. Eğer satır yeni eklenmişse (veritabanına eklenmiş ancak henüz kaydedilmemişse), INSERTED bayrağı 1 olur.
READ
	• Açıklama: Bu bayrak, satırın veritabanından okunup okunmadığını gösterir. Eğer satır veritabanından okunduysa, READ bayrağı 1 olur. Bu bayrak, özellikle veritabanından veri çekildiğinde kullanılır.
UPDATED
	• Açıklama: Bu bayrak, satır veritabanından okunduktan sonra güncellenip güncellenmediğini gösterir. Eğer satır veritabanından okunduktan sonra bir değişiklik yapılmışsa, UPDATED bayrağı 1 olur. Aksi takdirde 0 olur.



--SATIRLARI KALDIRMA

CLEAR ROW | ALL {table};
CLEARTABLE {table};
CLEARTABLE {table} WHERE {condition};
CLEARTABLE {table} CRITERIA COLUMNS {columns}  VALUES {values} [NOTCASESENSITIVE];

--STUNLARI KALDIRMA

Tüm sütunları kaldırmak için :  DESTROYTABLE {table};
Tek bir sütunu kaldırmak için : REMOVE COLUMN {columnname} [PERMANENT] FROM {table};


	- COPY STRUCTURE komutu, bir tablo değişkeninin yapısını okumak için kullanılır.

Tablonun seçili satır sayısını döndüren fonk:  SELECTEDROWCOUNT()
Verilen tablonun sütun sayısını okumak için fonk: GETCOLUMNCOUNT()


--  TABLOLAR ARASI VERİ AKTARIMI

 *  Tablo Kopyalama:
Bir tablonun tüm yapısını ve verilerini kopyalamak için COPY TABLE komutu kullanılır. 

    COPY TABLE {sourcetable} INTO {destinationtable} [WITHFLAGS];  

 *  Hücre Satır Verilerini Kopyalama:
TMPTABLE_CLIENT = SOURCE_CLIENT;   -- bu şekilde aktarma yapabiliriz ancak toplu işlemlerde bunu kullanmak mantıklı değil.

MOVE-CORRESPONDING {sourcetable} TO {destinationtable} [WITHFLAGS];  -- iki tablonun da alanları aynı olmalı bu şekilde direkt kopyalama yapabiliriz
   ÖRNEĞİN ;

    OBJECT:
            TABLE SOURCE,
            TABLE TMPTABLE;
    /* source table with 3 columns */
    SELECT CLIENT,USERNAME,CREATEDBY, CREATEDAT
            FROM IASUSERS
            WHERE USERNAME LIKE 'BTAN%'
            INTO SOURCE;
    /* destination table with 5 columns*/
    SELECT CLIENT,USERNAME,CREATEDBY, PWDVALIDITY
            FROM IASUSERS
            WHERE 1=2
            INTO TMPTABLE;
    APPEND ROW TO TMPTABLE;
    /* move all corresponding columns */
    MOVE-CORRESPONDING SOURCE TO TMPTABLE;

Ek olarak, tüm satır tabanlı bayraklar hem kaynak hem de hedef satırlarda bulunur, bu nedenle bir satırı tanımlama tablosuna aktarırken bayrak değerleri de dikkate alınmalıdır. Varsayılan olarak, MOVE-CORRESPONDIG komutu bayrak değerlerini aktarmaz, ayrıca satır bayraklarını da aktarmanız gerekiyorsa, COPY TABLE komutu gibi WITHFLAGS varyasyonunu kullanmanız gerekir. 


--
Genellikle, MOVE-CORRESPONDING komutu bir LOOP deyiminde kullanılır ve kaynak tablodaki her satır için, hedef tabloya eklenen yeni bir satır veya koşullu bir ifade nedeniyle kaynak tabloya aktarılan satırlar kullanılır. Bu gibi durumları kolaylaştırmak için, verilen koşul nedeniyle kaynak tablonun satırlarını aktaran MERGETABLE komutu kullanılır. MERGETABLE komutu, LOOP staments gibi ek bir karma indeks varyasyonu ile CLEARTABLE komutuna benzer bir komuttur.
    
    MERGETABLE {source} INTO {destination} [WITHFLAGS] WHERE {condition};
    MERGETABLE {source} INTO {destination} [WITHFLAGS]
                        CRITERIA COLUMNS {cols} VALUES {vals} [NOTCASESENSITIVE];
    MERGETABLE {source} INTO {destination} [WITHFLAGS]
                        CRITERIA INDEXED {index} VALUES {vals};


-- LOOP 

LOOP AT table [WHERE {condition}]
BEGIN
        block
ENDLOOP;

LOOP AT {table} CRITERIA COLUMNS {columns} VALUES {values} [NOTCASESENSITIVE]
BEGIN
        block
ENDLOOP
/*veimlilik ve hız daha yüksek where yerine crıterıa kullan*/
/* {columns} & {values} are comma separated list. */
 
 örnek : 

      OBJECT:
              TABLE T1,
              STRING RESULT,
              STRING STRCREATEDBY;
      SELECT USERNAME, CREATEDBY, PWDVALIDITY
              FROM IASUSERS
              INTO T1;
      STRCREATEDBY = 'BTAN';
      RESULT = '';
      APPEND ROW TO T1;
      T1_USERNAME = 'NewUser';
      T1_CREATEDBY = 'BTAN';
      T1_CREATEDBY = 30;
      LOOP AT T1 CRITERIA COLUMNS CREATEDBY,INSERTED VALUES STRCREATEDBY,1
      BEGIN
              RESULT  = RESULT + T1_USERNAME + ':';
              RESULT = RESULT  + T1_PWDVALIDITY + TOCHAR(10);
      ENDLOOP;


!! 
BUILDHASHINDEX {indexname} COLUMNS {columns} ON {table} [FORCE];

• Bu komut, USERS tablosunda, USER_ID ve EMAIL sütunları için bir hash index oluşturur.
• USER_ID_INDEX ismiyle yeni bir hash index oluşturulur.
• FORCE seçeneği kullanıldığı için, daha önce var olan aynı indeks varsa, üzerine yazılacaktır.


 örnek : 
 
    OBJECT:
        TABLE T1,
        STRING RESULT,
        STRING INDEXNAME;
    SELECT USERNAME, CREATEDBY,PWDVALIDITY
        FROM IASUSERS
        INTO T1;
    INDEXNAME = 'myindex';
    RESULT = '';
    BUILDHASHINDEX INDEXNAME COLUMNS PWDVALIDITY,CREATEDBY ON T1;
    LOOP AT T1 CRITERIA INDEXED INDEX INDEXNAME VALUES 2000, 'BTAN'
    BEGIN
            RESULT  = RESULT + T1_USERNAME + ':';
            RESULT = RESULT  + T1_PWDVALIDITY + TOCHAR(10);
    ENDLOOP;
    RESULT = RESULT + '----------------' + TOCHAR(10);
    LOOP AT T1 CRITERIA INDEXED INDEX INDEXNAME VALUES 60, 'kkizir'
    BEGIN
            RESULT  = RESULT + T1_USERNAME + ':';
            RESULT = RESULT  + T1_PWDVALIDITY + TOCHAR(10);
    ENDLOOP;  



-- LOCATERECORD !!!!!
İki tablodaki verilerin karşılaştırılması için kullanılır.

LOCATERECORD SEQUENTIAL COLUMNS {columns} VALUES {values}
                                ON {table} [NOTCASESENSITIVE] [NEXT] [LAST];

-bulursa SYS_STATUS 0 olur ve actıverow orası olur 
-bulamazsa SYS_STATUS 1 olur


LOCATERECORD BINARYSEARCH COLUMNS {columns} VALUES {values}
                                  ON {table} [NOTCASESENSITIVE];

LOCATERECORD INDEXED INDEX {indexname} VALUES {values}
                                       ON {table} [NEXT] [LAST];


-- SORT : Verileri sıralamak
Bir veya daha fazla sütun nedeniyle satırları azalan ve artan düzende sıralamak mümkündür. Varsayılan sıralama artandır ve büyük/küçük harfe duyarlı değildir. 


    SORT {tablename} [CASESENSITIVE] ON [DESC] {column1}, [DESC] {column2};
 
 örnek : 

    OBJECT:
            TABLE TMPTABLE;
    SELECT USERNAME, CREATEDBY, CREATEDAT
    FROM IASUSERS
    INTO TMPTABLE;
    SORT TMPTABLE ON CREATEDBY, DESC CREATEDAT;
    /* this command will be discussed later */
    SET TMPTABLE TO TABLE TMPTABLE;
    
    SORT TMPTABLE ON @STRINGVAR3;

Ağaç benzeri bir tablo elde etmek için tabloları hiyerarşik bir şekilde sıralamak için SORT HIERARCHICAL varyasyonu kullanılır. 

SORT {table} HIERARCHICAL IDCOLUMN {idcolumn} PARENTIDCOLUMN {parentidcolumn}
                           [ROOTINDICATOR {indicatorvalue}] [MARKLEAFSASNODE]

 örnek : 

    SELECT USERNAME AS COUNTRY, CREATEDBY AS NAME
            FROM IASUSERS
            WHERE 1=2
            INTO TMPTABLE;
    APPEND ROW TO TMPTABLE;
    TMPTABLE_COUNTRY = 'TURKEY';
    TMPTABLE_NAME = 'IZMIR';
    APPEND ROW TO TMPTABLE;
    TMPTABLE_NAME = 'TURKEY';
    APPEND ROW TO TMPTABLE;
    TMPTABLE_COUNTRY = 'GERMANY';
    TMPTABLE_NAME = 'KARLSRUHE';
    APPEND ROW TO TMPTABLE;
    TMPTABLE_NAME = 'GERMANY';
    APPEND ROW TO TMPTABLE;
    TMPTABLE_COUNTRY = 'GERMANY';
    TMPTABLE_NAME = 'BERLIN';
    APPEND ROW TO TMPTABLE;
    TMPTABLE_COUNTRY = 'TURKEY';
    TMPTABLE_NAME = 'IZMIR';
    /* to sort same level items */
    SORT TMPTABLE ON NAME;
    SORT TMPTABLE HIERARCHICAL IDCOLUMN 'NAME' PARENTIDCOLUMN 'COUNTRY';
    /* this command will be discussed later */
    SET TMPTABLE TO TABLE TMPTABLE;

