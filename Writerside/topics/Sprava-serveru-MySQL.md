# Sprava-serveru-MySQL

## MySQL
- Při vytvoření se vytváří 2 db (**mysql** a test)
- V **mysql** jsou uloženy tabulky uživatelských účtů. Chová se jako
  jakákoliv DB. V tabulkách jsou uloženy veškerá oprávnění přidělená
  jednotlivým uživatelům.
- Většina sloupců obsahuje hodnoty YES or NO. 
- DB obsahuje tabulky jako jsou: User, Db, Host, Func, Colums_priv, Tables_priv

- **Import** 
  - Import dat do DB se provádí skrz mysqlimport (mysqlimport _Nejakadatabaze_ Tabulka_Do_Ktere_Chci_Nacist_Data.txt). Nebo příkaz **LOAD DATA INFILE**
- **Export**
  - Pro export se používá **mysqldump**. Obdoba programu mysqlimport. Lze exportovat celou DB nebo jen jednu tabulku. Příkaz **SELECT INTO OUTFILE**
![Export-mysql.png](Export-mysql.png)
### Typy tabulek
- **Netransakční**
  - MyISAM --> **Defaultní**
  - ISAM
  - MERGE
  - HEAP
- **Transakční**
  - BDB
  - InnoDB

### myisamcheck
- Program myisamchk slouží k údržbě (tedy k získávání informací, kontrole, opravám a optimalizaci) tabulek typu MyISAM
```SQL
myisamchk [přepínače] Název_Tabulky
```

### mysqladmin
- např. změna hesla, vytvoření či odstranění DB, zjištění informací o stavu a verze DB
![Mysqladmin.png](Mysqladmin.png)

### Co umět :
- Import/Export
- Vytvoření scriptu
- Loginy
- Server roles
- Users
- DB roles
- Vytvoření ER diagramu
