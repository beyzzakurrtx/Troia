
# 🔧 Troia – Temel Kontrol Yapıları

Troia IDE’de kullanılan temel kontrol yapıları ve döngülerin örneklerini içermektedir. Aşağıdaki yapılar ele alınmıştır:

IF / ELSE / ENDIF:

          IF A == 1 THEN
                        RESULT = 'A equals to one';
                ELSE
                        IF A < 1 THEN
                                RESULT = 'A is less than one';
                        ELSE
                                RESULT = 'A is more than one';
                        ENDIF;
                ENDIF;




SWITCH / CASE / DEFAULT / ENDSWITCH :

          OBJECT:
                STRING VAR,
                STRING RESULT;
        VAR = '8';
        
        SWITCH VAR
            CASE 5:         RESULT = 'It is five';
            CASE 6:         RESULT = 'It is six';
            CASE '7','8':   RESULT = 'It is seven or eight';
            DEFAULT:        RESULT = 'I do not know what it is.';
        ENDSWITCH;



LOOP AT / ENDLOOP:

        LOOP AT TMPTABLE
        BEGIN
            /* Burada her satır için yapılacak işlemler */
        ENDLOOP;

        

WHILE / ENDWHILE :

                OBJECT:
                INTEGER VAR,
                STRING RESULT;
        VAR = 1;
        RESULT = '';
        
        WHILE VAR < 10
        BEGIN
            IF VAR % 2 == 0 THEN
                RESULT = RESULT + VAR + ':even, ';
            ELSE
                RESULT = RESULT + VAR + ':odd, ';
            ENDIF;
            VAR = VAR + 1;
        ENDWHILE;

BREAK ve CONTINUE kullanımı :

                 OBJECT:
                INTEGER INDEXNUM,
                INTEGER ODDNUMBERSTOTAL,
                STRING ODDNUMBERS;
        
        ODDNUMBERSTOTAL = 0;
        INDEXNUM = 0;
        ODDNUMBERS = '';
        
        WHILE 1 == 1
        BEGIN
            INDEXNUM = INDEXNUM + 1;
        
            /* Döngüyü 10’da kır */
            IF INDEXNUM == 10 THEN
                BREAK;
            ENDIF;
        
            /* Çift sayılarda döngü başına atla */
            IF INDEXNUM % 2 == 0 THEN
                CONTINUE;
            ENDIF;
        
            ODDNUMBERSTOTAL = ODDNUMBERSTOTAL + INDEXNUM;
            ODDNUMBERS = ODDNUMBERS + INDEXNUM + ',';
        ENDWHILE;

Döngü 10’a ulaştığında BREAK ile sonlandırılır.

Çift sayılar CONTINUE ile atlanır, sadece tek sayılar toplanır ve stringe eklenir.


