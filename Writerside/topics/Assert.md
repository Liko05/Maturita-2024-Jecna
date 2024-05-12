# 24. Výjimky a aserce, debugování a zpracování chyb

## Výjimky

- Výjimka je objekt, který reprezentuje chybu nebo výjimečnou situaci
- Výjimky se používají k zastavení běhu programu
- Používají se k ošeření vstupů, chyb v datech, chyb v programu, atd.
- Výjimky se dělí na dvě kategorie:
    - **Kontrolované** - musí být zachyceny a zpracovány
    - **Nekontrolované** - nemusí být zachyceny a zpracovány
- Výjimky se zachytávají pomocí bloku `try-catch`
- Výjimky se vyhazují pomocí klíčového slova  `throw` či `throws`

```Java
try {
    // kód, který může vyhodit výjimku
} catch (Exception e) {
    // zpracování výjimky
}
```

```Java
public void method() throws Exception {
    // kód, který může vyhodit výjimku
    throw new Exception("Chyba!");
}
```

### Vlastní výjimky

- Vlastní výjimky se vytvářejí pomocí třídy `Exception`
- Vlastní výjimky se dědí z třídy `Exception`
- Můžeme tak udelat specifické výjimky pro náš program

```Java
public class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}
```

```Java
public void method() throws MyException {
    // kód, který může vyhodit výjimku
    throw new MyException("Chyba!");
}
```

## Aserce

- Jedná se o kontrolu stavů, které je nepřípustné, aby nastaly
- Zpomaluje program, proto se používá pouze v době vývoje
- Pokud dojde k chybě aserce, program se zastaví

```Java
assert (1 == 1);
```

```Java
assert (1 == 2) : "Chyba!";
```

## Debugování

- Debugování je proces hledání chyb či ověření flow programu
- Debugování se provádí pomocí debuggeru
- Provádí se pomocí breakpointů, které zastaví běh programu
- Debugger umožňuje sledovat hodnoty proměnných, stav zásobníku, atd.

```Java
public class Main {
    public static void main(String[] args) {
        int a = 1;
        int b = 2;
        int c = a + b;
    }
}
```

## Zpracování chyb

- Zpracování chyb je důležité pro uživatele, aby věděl, co se stalo
- Chyby se zpracovávají pomocí logování, výjimek, asercí
- Vyhazovat smysluplné chybové hlášky pro uživatele

```Java
try {
    // kód, který může vyhodit výjimku
} catch (Exception e) {
    System.out.println("Chyba: " + e.getMessage());
}
```