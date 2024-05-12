# 5. Architectural design patterns - MVC, Multitier, Monolithic, P2P, Client/Server

## MVC

- **MVC** - Model-View-Controller
    - **Model** - Data, která se zobrazují
    - **View** - Zobrazuje data
    - **Controller** - Zpracovává uživatelské vstupy

- ![MVC](https://media.geeksforgeeks.org/wp-content/uploads/20240219101004/MVC-Design-Pattern-.webp)

### Komunikace mezi vrstvami

- User Interaction s View
    - User interacts s view, tj. kliká na tlačítko, zadává text, atd.
- View získá data z User input
    - View získá data z User input a předá je Controlleru
- Controller zpracuje data z View
    - Controller zpracuje data z View
    - Rozhodne, co se má stát na základě těchto dat
- Controller updatne Model
    - Controller updatne Model na základě dat od Usera
- Model updatne View
    - Model updatne View, aby zobrazil nová data
- View si vyzvedne data z Modelu
    - View si vyzvedne data z Modelu a zobrazí je uživateli
- Controller updatne Viwe
    - Controller updatne View, aby zobrazil nová data
- View zobrazí data uživateli
    - View zobrazí data uživateli

```mermaid
graph TB
    User(User) -->|Interacts| View
    View -->|Passes User Input| Controller
    Controller -->|Processes Input| Model
    Model -->|Updates| View
    Controller -->|Updates| View
    View -->|Displays Data| User
```

- **Výhody**
    - **Separace zájmů** - Každá vrstva má jiný zájem
    - **Testovatelnost** - Každá vrstva je testovatelná samostatně
    - **Rozšířitelnost** - Každá vrstva je rozšířitelná samostatně
    - **Změny** - Změny v jedné vrstvě neovlivní ostatní vrstvy
- **Nevýhody**
    - **Složitost** - Může být složité implementovat
    - **Duplikace kódu** - Může dojít k duplikaci kódu

## Multitier

- **Multitier** - Rozdělení aplikace do více vrstev, každá má svůj úkol a bere se jako service.

- ![Multitier](https://media.geeksforgeeks.org/wp-content/uploads/20230519003319/Amia-Web-Tier-EJB-Tier.png)

- **Vrstvy:**
    - **Presentation Tier** - Zobrazuje data uživateli
    - **Business Logic Tier** - Zpracovává data
    - **Data Tier** - Ukládá data
    - **Communication Tier** - Komunikuje s jinými systémy

- **Výhody**
    - **Separace zájmů** - Každá vrstva má jiný zájem
    - **Testovatelnost** - Každá vrstva je testovatelná samostatně
    - **Rozšířitelnost** - Každá vrstva je rozšířitelná samostatně
    - **Změny** - Změny v jedné vrstvě neovlivní ostatní vrstvy
- **Nevýhody**
    - **Složitost** - Může být složité implementovat

```mermaid
graph TB
    User(User) -->|Interacts| Presentation
    Presentation -->|Passes User Input| Business
    Business -->|Processes Input| Data
    Data -->|Updates| Business
    Business -->|Updates| Presentation
    Presentation -->|Displays Data| User
```

## Monolithic

- **Monolithic** - Všechny části aplikace jsou v jednom celku.

- **Výhody**
    - **Jednoduchost** - Jednoduché na implementaci
    - **Rychlost** - Rychlejší než multitier
    - **Testovatelnost** - Snadnější testování
- **Nevýhody**
    - **Škálovatelnost** - Špatná škálovatelnost
    - **Rozšířitelnost** - Špatná rozšířitelnost
    - **Změny** - Změny v jedné části mohou ovlivnit celou aplikaci
    - **Testovatelnost** - Testování celé aplikace najednou
    - **Složitost** - Složité na údržbu
    - **Špatná organizace** - Špatná organizace kódu

```mermaid
graph TB
    User(User) -->|Interacts| Monolithic
    Monolithic -->|Processes Input| Monolithic
    Monolithic -->|Updates| Monolithic
    Monolithic -->|Displays Data| User
```

## P2P

- **P2P** - Peer-to-Peer, kde každý uživatel je zároveň serverem a klientem.

- ![P2P](https://i.stack.imgur.com/XYnkg.png)

- **Výhody**
    - **Škálovatelnost** - Dobrá škálovatelnost
    - **Rychlost** - Rychlé přenosy dat
    - **Bezpečnost** - Bezpečnostní výhody
- **Nevýhody**
    - **Špatná organizace** - Špatná organizace kódu
    - **Bezpečnost** - Bezpečnostní rizika
    - **Špatná škálovatelnost** - Špatná škálovatelnost
    - **Složitost** - Složité na implementaci

```mermaid
graph TB
    User1(User1) -->|Sends Data| User2
    User2 -->|Sends Data| User1
```

## Client/Server

- **Client/Server** - Klient požaduje data od serveru a server mu je poskytuje.

- ![Client/Server](https://static.javatpoint.com/core/images/socket-programming.png)

- **Typy:**
    - **Thin Client** - Klient má minimální funkce a většina je na serveru
    - **Thick Client** - Klient má většinu funkcí a server je pouze pro data
    - **Hybrid Client** - Kombinace Thin a Thick Client
- **Vrstvy:**
    - **Client** - Klient, který požaduje data
    - **Server** - Server, který poskytuje data
    - **Database** - Databáze, kde jsou data uložena
- **Výhody**
    - **Škálovatelnost** - Dobrá škálovatelnost
    - **Bezpečnost** - Bezpečnostní výhody
    - **Rychlost** - Rychlé přenosy dat
- **Nevýhody**
    - **Složitost** - Složité na implementaci

```mermaid
graph TB
    User(User) -->|Requests Data| Server
    Server -->|Sends Data| User
```