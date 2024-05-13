# Bezpecnost-a-uzivatelska-opravneni-a-role

## Otázky
- proč zabezpečit DB
- způsoby
- 2 úrovně zabezpečení
- Co je to role
- Jak se vytváří role
- Jáké default role znáš
## Bezpečnost DB
- db je třeba zabezpečit na několika levelech
- software i hardware
  - samotná data
  - DBMS
  - aplikace spojené s DB --> zabránit SQL injections apod.
  - lokaci kde je server
- 3 základní pomyslné skupiny uživatelů
  - admin
  - vlastník DB
  - běžný uživatel
- je třeba každé z těchto skupi nastavit patřičná oprávnění
- nejzákladnějím zabezpečením je vytvoření **View** nad tabulkou a pracovat s tím místo tabulky

### Proč zabezpečit DB
- data jsou základem všeho, dost často jsou to i citlivá data
- neoprávněné vstupy do DB nás stojí peníze i čas
### Druhy obecného zabezpečení
- Hashing, authentikace, firewally, záloha dat
## 1. stupeň zabezpečení
- zabezpečit přístup na server jako takový --> **login**

a) windows autentifikace --> MSSQL
  Create login user from windows;
```SQL
Create login Franta from windows;
```
- wizzard

b) SQL authentifikace --> všechny DB
```SQL
Create login Franta with password = "password";
```
- wizzard 

## 2. stupeň zabezpečení
- přístup k databázi na serveru, řeší se tvorbou usera
- jeden login může mít žádný, nebo více username
```SQL
Create user Franta for login franta_login;
```

## MSSQL - uživatelská oprávění a role
- serverová role týkající se celého serveru --> předefinovány

## Role
- **soubor práv**
- GRANT Role
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON schema_name.table_name TO role_name;
```
### Server role 
- Práva vztahující se k celému serveru
- **sysadmin** - super uživatel
- **serveradmin** - konfiguruje nastavení celého serveru
- **setupadmin** - správa Linked servers a s tím související práva
- **securityadmin** - správa uživatelů a práv
- **processadmin** – správa procesů
- **dbcreator** - vytváření a změna databází
- **diskadmin** - správa diskových souborů
- **bulkadmin** - vykonávání SQL dotazu BULK INSERT
### Databázové role 
- práva, která se vztahují k jedné konkrétní DB
- tyto role jde vytvářet, měnit nebo mazat
- **public** - všichni uživatelé dané databáze jsou do ní zařazení, reprezentuje výchozí práva pro kohokoliv
- **db_owner** - superuživatel vůči dané databázi, zahrnuje práva všech níže uvedených rolí
- **db_accessadmin** - správa uživatelů
- **db_datareader** - povoleno čtení všech dat ve všech tabulkách od všech uživatelů
- **db_datawriter** - povolen zápis, změna a mazání dat ve všech tabulkách od všech uživatelů
- **db_ddladmin** - přidání, změna a odstraňování všech objektů v databázi
- **db_securityadmin** - správa rolí, jejich členů a práv
- **db_backupoperator** - práva na zálohování databáze
- **db_denydatareader** - zákaz čtení dat z databáze
- **db_denydatawriter** - zákaz změny dat v databázi


![role-script.png](role-script.png)
## Sum-up
- **Bezpečnost** --> hw is sw
  - zabezpečení serveru - **login** (windows - MSSQL a SQL pro vše ostatní)
  - přístup k databázi na serveru - **tvorba usera**
- **Role** --> soubor práv
  - Server
  - Databazové