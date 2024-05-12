# 3. Algoritmizace - Rekurze, Brute Force, Heuristiky, Nedeterministické algoritmy

- Algoritmy jsou postupy řešení problémů pro jednotlivé problémy.
- Každý algoritmus má svou složitost, která se dá vyjádřit časovou a paměťovou složitostí.
- Zásadně je tvořen jednoznačným postupem, zaručuje že pro správný vstup vrátí správný výstup.

## Vlastnosti algoritmů

- **Hromadnost** - Měnitelná vstupní data.
- **Determinovanost** - Každý krok je jednoznačně definován.
- **Konečnost a resultativnost** - Pro správný vstup vrátí správný výstup.

## Rekurze

- **Rekurze** je způsob, jak se funkce volá sama.
- **Potenciální problémy:**
    - Rekurze může způsobit přetečení zásobníku, pokud je rekurze příliš hluboká.
    - Rekurze se může stát neefektivní, pokud se stejné hodnoty počítají vícekrát.
    - Rekurze se může zacyklit, pokud není správně implementována.
- **Výhody rekurze**- Rekurze může být jednodušší na pochopení a implementaci než iterativní řešení.

- **Možné rekurze**:
    - **Přímá rekurze** - Funkce volá sama sebe.
    - **Nepřímá rekurze** - Funkce volá jinou funkci, která zase volá původní funkci.

- **Příklad rekurze**:
    - **Faktoriál** - Faktoriál je součin všech kladných celých čísel menších nebo rovných n.
      ```Java
      int factorial(int n) {
      if (n == 0) return 1;
      return n * factorial(n - 1);
      }
        ```
    - **Fibonacciho posloupnost** - Fibonacciho posloupnost je posloupnost čísel, kde každé číslo je součtem dvou
      předchozích čísel.
      ```Java
      int fibonacci(int n) {
      if (n <= 1) return n;
      return fibonacci(n - 1) + fibonacci(n - 2);
      }
         ```

## Brute Force

- **Brute Force** je jednoduchá metoda řešení problémů, která vyzkouší všechny možné kombinace.
- **Výhody Brute Force**:
    - Vždy najde správné řešení.
    - Dá se používat v mnoho směrech a pro mnoho úloh.
    - Typicky je používán na malé a jednoduché problémy.
- **Nevýhody Brute Force**:
    - Může být velmi pomalý protože vyzkouší všechny možné kombinace.

### Typy Brute Force

- **Vyčerpávající prohledávání** - Vyzkouší všechny možné kombinace.
- **Hledání do hloubky** - Prohledává všechny možné cesty.
- **Hledání do šířky** - Prohledává všechny možné cesty v dané hloubce.
- **Backtracking** - Vyzkouší všechny možné kombinace a vrátí se zpět, pokud není správná.

## Heuristiky

- **Heuristiky** jsou postupy, které používá praktické řešení problémů namísto optimálního řešení. Často se používají na
  problémy, které nemají optimální řešení, nebo jsou až moc komplexní aby byly řešeny optimálně.
- **Výhody heuristik**:
    - Může být použitelný na problémy, které nemají optimální řešení.
    - Může být použitelný na problémy, které jsou příliš složité na optimální řešení.
- **Nevýhody heuristik**:
    - Nemusí vždy najít správné řešení.
    - Může být pomalý.
    - Může být obtížné určit, kdy je správné použít heuristiku.

- **Detekce virů:**
    - **Statická** - Prozkoumá kód podezřelého souboru a následně porovná s podozřelými vzory uloženými v databázi.
    - **Dynamická** - Izoluje podezřelý soubor do VM nebo karantény a dovolí antivirovém programu sledovat jeho chování.

## Nedeterministické algoritmy

- **Nedeterministické algoritmy** jsou algoritmy, které mohou mít více výstupů pro stejný vstup. Může volit pro více
  možností dalších kroků. Tímto se liší od deterministických algoritmů, které mají pro stejný vstup vždy stejný výstup.
- **Pomocí zkoumání výsledku lze určit:**
    - Zda existuje aspoň jedno řešení vyhovující zadání. Příkladem je nedeterministický konečný automat.
    - Pravděpodobnost provedení některých krokl algoritmu, pokud jsou známy pravděpodobnosti výberu dalších kroků.
      Příkladem může být teorie hromadné obsluhy.
- **Využití:**
    - **Nalezení aproximace řešní** - Nedeterministické algoritmy se používají pro hledání aproximace optimálního
      řešení.
    - **Konečný automat** - teoretický výpočetní model, který může mít více výstupů pro stejný vstup.
    - **Problém obchodního cestujícího** - Problém nalezení nejkratší cesty, která navštíví všechny města a vrátí se
      zpět na začátek.