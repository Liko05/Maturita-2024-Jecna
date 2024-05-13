# Ulozene-procedury-a-funkce

## Otázky
- co je to procedůra
  - kde se ukládá
  - jak se volá 
- výhody a nevýhody procedůr
- co je to funcke

## Uložené procedůry
- Procedůra je metoda, která se **ukládá** do paměti v dané DB --> na **serveru**
- je to sada příkazů SQL
- ekvivalent metod z jiných programovacích jazyků
- Lze ji **opakovaně volat**
- umožňuje jak **vstupní** tak **výstupní parametry**
- při prvním zavolání se procedura uloží do cache odkud se pak volá

### Výhody
- je na straně serveru
- předkompilované provedení
- zvýšný výkon při častějším volání
- omezení počtu připojení klientů k aplikaci --> menší traffic
- zlepšuje se **škálovatelnost**
- bezpečnost --> místo práv na DQL můžeme dát práva jen na procedury

### Nevýhody
- v některých DB neexistuje debugging pro procedůry
- **nejsou přenositelné** mezi DB prostředím
- mívají zdrojový kód, který je přístupný uživateli
- přesouvání aplikační logiky na databázovou vrstvu se aplikace
  znepřehledňuje
- pokud jdeme podle best-practice bude v DB hrozně moc procedůr

![procedury-tabulka.png](procedury-tabulka.png)
## Sum-up
- **Procedůra** --> sada příkazů SQL, uložených **na serveru**. Lze ji volat opakově. Ekvivalent metod (třeba  z javy)
  - **výhody** --> je na serveru, zvýší výkon, bezpečnost
  - **nevýhody** --> nepřenositelné mezi DB, nepřehlednost, je jich hodně
