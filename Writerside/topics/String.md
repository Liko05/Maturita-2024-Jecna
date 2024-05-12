# 25. Zpracování a parsování textových dat, regulární výrazy, kódování a stringy

- Jedná se o textová data typu `String`, která mohou být zpracována a parsována.
- Jelikož je to object, má funkce, např. `.size()`, `.charAt()`, `.substring()`, `.replace()`...
- Má tolik byte, kolik má znaků, ale v paměti zabírá více, protože každý znak je v Unicode.
- Existuje `StringBuilder` a `StringBuffer`, které jsou mutable, na rozdíl od `String`.
  `mutable` znamená, že se může měnit

## Zpracování a parsování textových dat

### Zpraování textových dat

- Jedná se o manipulaci s textem, který je uložen v proměnné typu `String`.
- Zpracování textu může být prováděno pomocí metod, které jsou dostupné v třídě `String`.
- Můžeme s textem provádět různé operace, jako je například vyhledávání, nahrazování, porovnávání, spojování,
  rozdělování, ...

`replace()` - nahradí všechny výskyty daného znaku nebo podřetězce jiným znakem nebo podřetězcem
`split()` - rozdělí řetězec na podřetězce podle zadaného oddělovače
`substring()` - vrátí podřetězec z původního řetězce
`toLowerCase()` - převede všechny znaky na malá písmena
`toUpperCase()` - převede všechny znaky na velká písmena
`trim()` - odstraní bílé znaky na začátku a na konci řetězce

### Parsování textových dat

- Parsování textových dat je proces, kdy se textový řetězec převede na jiný datový typ.

`Integer.parseInt()` - převede řetězec na celé číslo
`Double.parseDouble()` - převede řetězec na desetinné číslo
`Boolean.parseBoolean()` - převede řetězec na logickou hodnotu

- Pokud se nepovede parsování, tak se vyhodí výjimka `NumberFormatException`.

## Regulární výrazy

- Umožňují kontrolovat, jestli daný řetězec obsahuje nebo neobsahuje určitý pattern
- Používáme zásadně k ošetření vstupních dat od uživatele či validaci dat
- V Javě se používají třídy `Pattern` a `Matcher` z balíčku `java.util.regex`

### Základní znaky

- Příklad: `String pattern = "^[a-zA-Z0-9]*$";`

`^` - začátek řetězce
`$` - konec řetězce
`.` - libovolný znak
`[abc]` - znak a, b nebo c
`[^abc]` - znak, který není a, b nebo c
`[a-z]` - znak od a do z
`[a-zA-Z]` - znak od a do z nebo od A do Z
`[0-9]` - číslice od 0 do 9

### Pattern

- Třída `Pattern` reprezentuje regulární výraz
- Metoda `compile()` vytvoří instanci třídy `Pattern` z řetězce

```java
Pattern pattern = Pattern.compile("^[a-zA-Z0-9]*$");
```

### Matcher

- Třída `Matcher` reprezentuje nalezený pattern v řetězci
- Vyhledává pattern v textovém řetězci

```java
Matcher matcher = pattern.matcher("Hello123");
boolean match = matcher.matches();

while (matcher.find()) {
    System.out.println("Match: " + matcher.group());
}
```