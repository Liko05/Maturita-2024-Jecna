# Jazyk-SQL-SELECT-VIEW

## Otázky
- Co je to SELECT a k čemu je 
- Co je to VIEW a k čemu je
- Jaké znáš agregáční funcke
- K čemu je JOIN a jeho druhy
## Select
- příkaz pro **zobrazení dat v DB**
- zobrazí data z jedné nebo více tabulek
- můžeme použít podmínky **WHERE, HAVING, GROUP BY, ORDER BY**
![Select-script.png](Select-script.png)

### Where
- matematický operátor
- log operátory
- podle množiny
- podle vzoru
- not null
```SQL
SELECT *
FROM Orders
WHERE ProductID = 101;

```
### Order by
- řízení **řazení dat** při **výpisu**
- řazení vzestupně ASC nebo sestupně DESC
```SQL
SELECT CustomerID, SUM(Quantity) AS TotalQuantity
FROM Orders
GROUP BY CustomerID
HAVING SUM(Quantity) > 100
ORDER BY TotalQuantity DESC;
```
### Group by
- seskupený dotaz - pro každou skupinu vytvoří jednoduchý souhrn
```SQL
SELECT CustomerID, SUM(Quantity) AS TotalQuantity
FROM Orders
GROUP BY CustomerID; 
```
### Having
- je určen jako podmínka pro skupiny --> bez group by nemá smysl
- pracuje jako WHERE, ale může obsahovat Agragáční funkce

```SQL
SELECT CustomerID, SUM(Quantity) AS TotalQuantity
FROM Orders
GROUP BY CustomerID
HAVING SUM(Quantity) > 100;
```
![klauzule.png](klauzule.png)

#### Agregáční funkce
- funkce, které pracují s jedním argumentem a vrátí jen jednu výslednou hodnotu
- mohou být **POUZE** za **SELECT** nebo **HAVING**
- pro odstranění duplicit slouží **DISTINCT**
- **COUNT()** - vrací počet záznamů, parametr není důležitý - stačí *
- **MAX()** - vrací nejvyšší hodnotu, použití pro INT, VARCHAR, DATE 
- **MIN()** - vrací nejmenší hodnotu, použití pro INT, VARCHAR, DATE 
- **AVG()** - vrací aritmetický průměr, použití pro INT 
- **SUM()** - vrací součet záznamů, použití pro INT

## Spojení tabulek JOIN
- Spojování dvou a více tabulek pomocí JOIN

### INNER JOIN 
- výpis průniku množin dat  z obou tabulek
```SQL
SELECT druh.nazev, zvire.nazev
FROM zvire
INNER JOIN druh ON zvire.druh_id = druh.id; 
```
### LEFT(RIGHT) JOIN
- výpis všech dat z levé(pravé) tabulky a průnik
```SQL
SELECT druh.nazev, zvire.nazev
FROM zvire
LEFT JOIN druh ON zvire.druh_id = druh.id;
```
### OUTER JOIN
- výpis všech dat z obou tabulek --> sjednocení množin
```SQL
SELECT druh.nazev, zvire.nazev
FROM zvire
FULL OUTER JOIN druh ON zvire.druh_id = druh.id;
```

![Joins.png](Joins.png)
## View
- **Virtuální** tabulka sestavená z výsledků SQL příkazu, definice je uložena na straně serveru
- bývá často kombinací více tabulek v DB (pomocí JOIN)
- můžeme opakovaně volat bez nutnosti opakovaného psaní SQL Selectů
- má stejnou syntaxi jako SELECT
- **neobsahuje skutečná data**, ale slouží k uložení často používaných nebo složitých selectů, jeden VIEW = jeden SELECT
- slouží také jako ochraný mechanismus, který dovolí uživatelům pouze přístup k viditelným datům ve VIEW nikoliv ke skutečným datům v tabulce
![View-script.png](View-script.png)
## Sum-up
- Select --> výpis dat z db
- View --> **virtuální tabulka** uložená na serveru. Bezpečnost dat. **Neobsahuje skutečná data**
- WHERE, GROUP BY, HAVING, ORDER BY
- Agregáční funkce --> funkce co mají na vstupu 1 atribut a vrací 1 výsledek
- **JOIN** - INNER, OUTER, LEFT/RIGHT