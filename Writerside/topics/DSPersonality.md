# 23. Vlastnosti datových struktur - Seřazenost a opakování prvků, Indexace, hashování a klíče prvků

## Seřazenost a hash

- Seřazenost prvků může být vzestupná nebo sestupná
- Objekty které jsou ukládány do datové struktury mohou být unikátní nebo se mohou opakovat
- SortedSet je datová struktura, která ukládá prvky ve vzestupném pořadí a neumožňuje opakování prvků
- HashSet je datová struktura, která ukládá prvky do hashovací tabulky a neumožňuje opakování prvků
- Funguje na principu hashování, kde se každý prvek ukládá na základě jeho hashovací hodnoty, pokud se hashovací hodnoty
  shodují, tak se prvek uloží na stejný index v tabulce

```Java
// write the hash method
public class Main {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Hello");
        set.add("World");
        set.add("Hello");
    }
}
```

- Výstup bude `[Hello, World]`, protože HashSet neumožňuje opakování prvků

```Java
private boolean hash(Object o) {
    return o.hashCode() % 10;
}
```

- Metoda `hashCode` vrací hashovací hodnotu objektu, která se používá pro uložení objektu do hashovací tabulky

## SortedSet

- Každý prvek je uložen nejvýše jednou
- generická datová struktura, která ukládá prvky ve vzestupném pořadí

## LinkedList

- Datová struktura, která ukládá prvky do spojového seznamu
- Každý prvek obsahuje odkaz na následující prvek
- Umožňuje opakování prvků
- Není seřazená

## Queue

- Datová struktura, která ukládá prvky do fronty
- Prvky se ukládají na konec fronty a odebírají se z jejího začátku
- FIFO - First In First Out
- Umožňuje opakování prvků
- Není seřazená

## Stack

- Datová struktura, která ukládá prvky do zásobníku
- Prvky se ukládají na konec zásobníku a odebírají se z jeho konce
- LIFO - Last In First Out
- Umožňuje opakování prvků
- Není seřazená

## Array

- Datová struktura, která ukládá prvky do pole
- Prvky se ukládají na základě indexu
- Umožňuje opakování prvků
- Není seřazená

## Map

- Datová struktura, která ukládá prvky do tabulky
- Každý prvek má klíč a hodnotu
- Klíč je unikátní
- Umožňuje opakování hodnot
- Není seřazená

## Set

- Datová struktura, která ukládá prvky do tabulky
- Každý prvek je unikátní
- Není seřazená
- Umožňuje opakování prvků