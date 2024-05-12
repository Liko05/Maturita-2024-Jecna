# 20. Testování, Unit testování a dokumentace zdrojového kódu

- Slouží jako proces ověření správnosti funkcionality vytvořeného kódu
- Rozlišujeme unit testy, integrační testy, systémové testy...

## Unit testování

- **Unit testing** se zaměřuje na testování jednotlivých komponent (unitů) programu, tedy jednotlivé funkce či metody
- Provádějí se v izolaci od zbytku kódu a ostatních komponent
- **Testovací frameworky** (JUnit, Mockito).. poskytují nástroje pro jednoduché psaní a spouštění testů

**Příklad:**

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class CalculatorTest {
    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        assertEquals(4, calculator.add(2, 2));
    }
}
```

## Integrační testování

- **Integrační testování** se zaměřuje na testování interakcí mezi jednotlivými komponentami programu
- Testuje se, zda jednotlivé komponenty spolu správně komunikují a spolupracují
- **Mockování** - nahrazení reálných komponent falešnými, které simulují jejich chování

**Příklad:**

```java
public class Calculator {
    private final Adder adder;

    public Calculator(Adder adder) {
        this.adder = adder;
    }

    public int add(int a, int b) {
        return adder.add(a, b);
    }
}
```

```java
public class Adder {
    public int add(int a, int b) {
        return a + b;
    }
}
```

```java
import org.junit.Test;

import static org.mockito.Mockito.mock;
import static org.mockito.Mockito.when;
import static org.junit.Assert.assertEquals;

public class CalculatorTest {
    @Test
    public void testAdd() {
        Adder adder = mock(Adder.class);
        when(adder.add(2, 2)).thenReturn(4);

        Calculator calculator = new Calculator(adder);
        assertEquals(4, calculator.add(2, 2));
    }
}
```

## Dokumentace zdrojového kódu

- **Dokumentace zdrojového kódu** slouží k popisu funkcionality a struktury kódu
- Kód dokumentujeme kvůli usnadnění jeho pochopení a údržby
- Dále díky dokumentaci můžeme zjistit, zda-li kod nelze napsat lépe, ulehčí budoucí rozvoj metody etc..
- **Javadoc** - nástroj pro generování dokumentace z komentářů ve zdrojovém kódu

**Příklad:**

```java
/**
 * Třída reprezentující kalkulátor.
 */
public class Calculator {
    /**
     * Sečte dvě čísla.
     *
     * @param a první číslo
     * @param b druhé číslo
     * @return součet čísel
     */
    public int add(int a, int b) {
        return a + b;
    }
}
```

### Programátorská a uživatelská dokumentace

- **Programátorská dokumentace** - popisuje strukturu a funkce kódu, určena pro vývojáře
- **Uživatelská dokumentace** - popisuje použití programu, určena pro uživatele

## Test reporty

- **Test reporty** slouží k zaznamenání výsledků testování
- Většinou vytváří někdo jiný než ten, psal daný kód
- **Code coverage** - měří, kolik procent kódu bylo otestováno

- **Vlastnosti test reportu:**
    - Testovací software a verze
    - Datum a čas testování
    - Seznam testů a jejich výsledky
    - Popis testované metody a očekávaného výsledku
    - Popis prostředí, ve kterém byly testy provedeny
    - Identifikace testovacích scénářů a testovacích dat
    - Výsledky testování a zjištěné chyby