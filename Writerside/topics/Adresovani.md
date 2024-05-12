# 1. Adresování a správa paměti - Garbage collecting, Reference/ukazatele, Struktura paměti programu

- V Javě se o správu paměti starat nemusíme, protože se o ni stará garbage collector. V C# se o správu paměti stará
  garbage collector, ale můžeme si s ním pomoci.
- Java funguje na principu zásobníku (Stack memory)

![Stack memory](https://miro.medium.com/v2/resize:fit:717/1*sG2wIZg7SqyhKMKD1jxM9A.png)
![Heap memory](https://journaldev.nyc3.cdn.digitaloceanspaces.com/2014/05/Java-Memory-Model.png)

## Method area

- Část paměti, ve které se ukládají informace o trídách, metodách a interfacech
- Jsou odtud trídy načítány
- Nachází se zde binary code tříd, statické a globální proměnné...

## String pool

- Místo, na kterém se ukládají `String`, které jsou vytvořeny pomocí `new`
- Pokud jsou vytvořeny dva stringy se stejným obsahem, tak se uloží pouze jeden string a druhý bude ukazovat na něj

```Java
String s1 = "Hello"; // vytvoří se string literal
String s1 = "Hello"; __ // s1 bude ukazovat na stejný string
```

## Heap space

- Zabírá největší část RAMky
- Ukládají se zde všechny objekty, které se během vývoje vytvářejí
- Dělí se na více částí, přesouvá objekty mezi nimi
    - Young generation
    - Old generation

### Young generation

- Dvě části:
    - Eden space
    - Survivor space
- Všechny nově vytvořené objekty se ukládají do Eden space
- Pokud je Eden space plný, proběhne GC, pokud je objekt používám dlouho, přesune se do Old generation
- V survivor space se ukládají objekty, které přežily Minor GC

### Old generation

- Obsahuje dlouho žijící objekty, které přežily několik GC
- Pokud je Old generation plný, proběhne Major GC

## PermGen

- Uchovává informace o metadatech, které JVM vyžaduje k opisu tříd a metod
- Příkladem je například deklarace třídy, metody...
- PermGe je součástí Heapu

## Native Method Stack

- Zaměřuje se na spuštění programu, které jsou psáný v jiných jazycích než Java
- Oddělen od jiných stacků

## Metaspace

- Nemá vrchní limit, má se vyvarovat OutOfMemoryError
- Pokud přeroste více než naše RAMka, tak použije virtuální paměť

## Stack memory

- princip LIFO
- Ukládají se frames, které obsahují informace při spuštění metody -> parametry o lokální proměnné
- Reference na objekty na Heapu a také primitivní proměnné (int, char, boolean...)

## Registry

- Ukládání adres instrukce, která se aktuálně provádí
- Instrukce je příkaz pro procesor , uchovává kvůli správnému pořadí
- Řeší i výjimky, neboť ukazují na poslední instrukci, která byla provedena

## Garbage collecting

- Proces, ve kterém se zbavujeme nepotřebných dat v paměti
- Java má automatický garbage collector, který se stará o správu paměti
- Nepoužívané objekty jsou označeny a smazány -> Nemá na sobě žádné reference
- Používanž objekt -> má na sobě reference

- Dělí se na:
    - Minor GC
    - Major GC

### Minor GC

- Probíhá v Young generation
- Proběhne když je odebrán nepoužívaný objekt nebo je pamět plná

**Příklad:**

```Java
public class GCExample {
    public static void main(String[] args) {
    Integer i1 = new Integer(10);
        i = null;
    }
}
```

### Major GC

- Probíhá v Old generation
- Stává se když přežijí Minor GC a jsou zkopírovány do Old generation
- Trvá déle než Minor GC

**Příklad:**

```Java
public class GCExample {
    public static void main(String[] args) {
    System.gc();
    Runtime.getRuntime().gc();
    }
}
```

### Jak probíhá GC

- GC se volá když je pamět v Eden space plná
- Používá se na prvky, které nemají referenci
- Pokud mají referenci, přesunou se do S0
- Při dalším GC se stane to samé, ale všechny prvky, které mají referenci se přesunou do S1 
- Přesunou se i ty, které jsou v S0 a smaže se celá S0
- Pokud prvky preskočí 8krát, přesouvají se do Old generation

## Reference a pointery

- Reference je adresa, která odkazuje, kde je metoda, objekt nebo proměnná v paměti uchována
- Pointer je to v Javě to samé
- Pokud vytvoříme objekt, udělá se nám v Heap paměti místo, ke kterému ukazuje reference

## Referenční proměnné

- Používají se k získaní objektu či hodnot
- Pokud vytváříme instanci objektu, tak sama instance je referenční proměnná, ukazuje na místo v paměti kde je uchován
- Reference jsou ukládány na Stacku

**Příklad:**

```Java
public class ReferenceExample {
    public static void main(String[] args) {
        TestTrida t1 = new TestTrida(); // t1 je referenční proměnná
    }
}
```