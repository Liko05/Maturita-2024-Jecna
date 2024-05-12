# 4. Anonymní metody (Lambda), speciální (magické) metody, statické metody, ukazatel na metodu (delegát)

## Anonymní metody (Lambda)

- **Anonymní metoda** je metoda, která nemá jméno a je definována přímo v místě, kde je použita.
- **Lambda výraz** je zjednodušený zápis anonymní metody, který se používá v mněkterých programovacích jazycích.
- **Příklad:**
  ```Java
    (a, b) -> a + b
    ```
- **Výhody:**
    - Zkracuje kód
    - Zvyšuje čitelnost kódu
    - Umožňuje předávat metodu jako parametr
    - Umožňuje definovat metodu v místě, kde je použita

## Speciální (magické) metody (dunder methods)

- **Speciální metody** jsou metody, které mají speciální význam a jsou volány automaticky v určitých situacích.
- **Příklady:**
    - `__init__` - konstruktor
    - `__del__` - destruktor
    - `__str__` - převedení objektu na řetězec
    - `__add__` - sčítání objektů
    - `__eq__` - porovnání objektů
    - `__len__` - délka objektu

- **Základní dunder metody**
    - objektová inicializace a reprezentace: `__init__`, `__repr__`, `__str__`
    - operátory porovnání: `__eq__`, `__lt__`, `__gt__`
    - logické operátory: `__bool__`
    - matematické operátory: `__add__`, `__sub__`, `__mul__`, `__truediv__`, `__floordiv__`, `__mod__`, `__pow__`
    - správa kontextu: `__enter__`, `__exit__`
- **Pokročilé dunder metody**
    - atributované a indoexované
      objekty: `__getattr__`, `__setattr__`, `__delattr__`, `__getitem__`, `__setitem__`, `__delitem__`
    - volání objektů: `__call__`
    - správa instancí: `__new__`, `__del__`
- **Speciální případy**
    - vytvoření uživatelsky definovaných kontejnerů: `__len__`, `__getitem__`
    - custom iterátory: `__iter__`, `__next__`
    - správa paměti a garbage collecting: `__del__`, `__delitem__`

### Příklad

```Python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f'Vector({self.x}, {self.y})'
```

## Statické metody

- **Statická metoda** je metoda, která nepatří k instanci třídy, ale k třídě jako celku.
- **Příklad:**
  ```Java
  public class Math {
      public static int add(int a, int b) {
          return a + b;
      }
  }
  ```
- **Výhody:**
    - Nepotřebuje instanci třídy
    - Zvyšuje čitelnost kódu
    - Umožňuje sdílet metodu mezi instancemi třídy
- **Nevýhody:**
    - Nemá přístup k instančním proměnným
    - Nemůže být přetížena
    - Nemůže být přepsána v potomcích

## Ukazatel na metodu (delegát)

- **Ukazatel na metodu** je objekt, který obsahuje referenci na metodu.
- **Příklad:**
  ```Java
  public class Button {
      private OnClickListener listener;

      public void setOnClickListener(OnClickListener listener) {
          this.listener = listener;
      }

      public void onClick() {
          if (listener != null) {
              listener.onClick();
          }
      }
  }

  public interface OnClickListener {
      void onClick();
  }
  ```

- **Výhody:**
    - Umožňuje předávat metodu jako parametr
    - Umožňuje definovat metodu v místě, kde je použita
    - Umožňuje vytvářet callbacky
- **Nevýhody:**
    - Může způsobit memory leak
    - Může způsobit problémy s vlákny
    - Může způsobit problémy s garbage collectingem