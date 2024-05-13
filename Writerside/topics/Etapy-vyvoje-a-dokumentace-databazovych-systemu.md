# Etapy-vyvoje-a-dokumentace-databazovych-systemu

## Otázky
- Popiš cyklus vývoje DS a jednotlivé etapy

## Životní cyklus DB
1. **Analýza**
a) analýza organizace
   - cílem je zjistit jak funguje firma a model reality, který chceme zpracovat. Bussiness rules, **dostupnost hardwaru a softwaru**
   - pokud už DB existuje zjistit jeji strukturu
b) definování problémů
   - HW a SW omezení
   - problémy současné DB
   - **přístupy** - práva/omezení v DB
   - **zálohování a archivace** dat
c) definování cílů
   - základní požadavky na funkcionalitu db
   - požadavky na role a zabezpečení
2. **Návrh**
   - vytváří se modely podle výsledků analýzy, **relační** a **logické schéma**
   - teoretická implementace nového systému - správa DB apod.
   - data musí poskytovat platné a přesné informace
   - musí splňovat funkční závislost a datové požadavky - **normalizace** aby nedocházelo k redudanci
3. **Implementace**
   - návrh se implementuje do konkrétního DS
   - optimalizace
   - nahrání **testovacích** dat
   - **import** a **export** dat, vyzkoušení uživatelských účtů
   - definice zálohování
4. **Testování**
   - **výkonost** a **spolehlivost** vstupů a výstupů
   - rychlost
   - zabezpečení přístupů k DB
   - **integrita dat**
   - nastavení záloh
5. **Provozání a údržba**
   - Nasazení db do produkce se reálnými daty

![zivotni-cyklus-db.png](zivotni-cyklus-db.png)
## Sum-up
- **Analýza** - sepsání požadavků a omození
- **Návrh** - schémata, základní funkčnost, normalizace
- **Implementace** - návrh se implementuje, optimalizace, import a export, zálohování
- **Testování** - přístupy, integrace, omezení, bezpečnost
- **Provoz a údržba** - nasazení do produkce s reálnými daty - support pro klienta