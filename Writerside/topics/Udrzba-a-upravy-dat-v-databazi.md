# Udrzba-a-upravy-dat-v-databazi

### Úprava dat v DB
a) kontrola integritních omezení
- Kontrola PK a rychlost vyhledávání
- Kontrola FK -> datový sirortci (neptaří žádnému PK)
- nemožnost snamzat ze strany 1 na straně N závislé záznamy (pokud není nastavená cascada)
- kontrola dat (vstupy) datový typ, rozsah, jednoznačnost, doménová integrita
b) kontrola normalizace
- provedení dostatečné normalizace
- každá entita zvlášť, 1NF nedodržena poznám podle rychlosti vyhledávání
- 2NF a 3NF nedodržené --> v db se nachází nadbytečná data
### Údržba dat v DB
- Databáze je pomalá idkyž integritní omezení a normalizace jsou splněny
a) vytvoření nových indexů nad místama, kde jsou často dotazy
b) pokud DB zabírá hodně místa --> dělat častěji zálohy/archivaci
c) ztráty vstupních dat, je nutn= zavést transakce
d) přístup uživatelům padá, přidám transakce, role, práva a omezení na minimum pro uživatele
