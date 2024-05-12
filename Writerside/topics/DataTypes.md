# 7. Datové typy, Generika, Výčtové datové typy, Struktury, Anotace, Operátory

## Datové typy

Datové typy jsou základnem programovacích jazyků. Každý jazyk má své vlastní datové typy, které se mohou
lišit v názvech, velikostech a významech. Datové typy mohou být rozděleny do několika skupin:

- **Primitivní datové typy** - jednoduché datové typy, které jsou přímo podporovány programovacím jazykem.
  Například celá čísla, desetinná čísla, znaky, logické hodnoty.
    - **Celá čísla** - `byte`, `short`, `int`, `long`
    - **Desetinná čísla** - `float`, `double`
    - **Znaky** - `char`
    - **Logické hodnoty** - `boolean`
    - **Speciální hodnoty** - `null`
    - **Speciální datové typy** - `String`, `BigInteger`, `BigDecimal`
- **Složené datové typy** - datové typy, které jsou složeny z primitivních datových typů.
  Například pole, struktury, třídy.
    - **Pole** - `int[]`, `double[]`, `String[]`
    - **Struktury** - `struct`
    - **Třídy** - `class`
    - **Generika** - `List<T>`, `Dictionary<K, V>`, `Queue<T>`, `Stack<T>`
    - **Výčtové datové typy** - `enum`
    - **Anotace** - `@Override`, `@Deprecated`, `@SuppressWarnings`
    - **Operátory** - `+`, `-`, `*`, `/`, `==`, `!=`, `&&`, `||`, `!`, `++`, `--`
    - **Speciální operátory** - `instanceof`, `new`, `this`, `super`, `?:`, `::`
    - **Speciální klíčová slova**
        - `abstract`, `final`, `static`, `synchronized`, `volatile`, `transient`, `native`, `strictfp`
        - `public`, `protected`, `private`, `package`, `import`, `class`, `interface`, `extends`, `implements`
        - `try`, `catch`, `finally`, `throw`, `throws`, `assert`, `break`, `continue`, `return`, `default`, `case`
        - `if`, `else`, `switch`, `case`, `default`, `while`, `do`, `for`, `foreach`, `goto`
        - `true`, `false`, `null`
        - `void`, `boolean`, `byte`, `char`, `short`, `int`, `long`, `float`, `double`

## Generika

- Generika jsou datové typy, které umožňují definovat třídy, rozhraní a metody s parametrizovanými typy.
    - Například seznam, slovník, fronta, zásobník.

```java
public class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }
}
```

```java
Box<Integer> box = new Box<>(42);
int value = box.getValue();
```

## Výčtové datové typy (Enum)

- Výčtové datové typy jsou datové typy, které umožňují definovat omezený počet hodnot.
    - Například dny v týdnu, barvy, roční období.

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```

```java
Day day = Day.MONDAY;
```

## Struktury

- Struktury jsou datové typy, které umožňují definovat vlastní datové struktury.
    - Například bod v rovině, obdélník, kruh.

```java
public struct Point {
    public int X { get; set; }
    public int Y { get; set; }
}
```

```java
Point point = new Point { X = 10, Y = 20 };
```

## Anotace

- Anotace jsou metadatové informace, které jsou připojeny k třídám, metodám, proměnným a dalším prvkům programu.
    - Například `@Override`, `@Deprecated`, `@SuppressWarnings`.

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
}
```

## Operátory

- Operátory jsou symboly, které provádějí operace nad daty.
    - Například sčítání, odčítání, násobení, dělení, porovnávání, logické operace.

```java
int a = 10;
int b = 20;
int c = a + b;
boolean d = a < b;
```