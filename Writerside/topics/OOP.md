# 14. Principy objektového programování, agregace a kompozice objektů

Objektově orientované programování (OOP) je programovací paradigma založené na konceptu "objektů", které mohou obsahovat
data a kód: data ve formě polí, často známých jako atributy; a kód, ve formě procedur, často známých jako metody.

## Základní principy OOP

1. **Abstrakce** - Abstrakce je proces skrývání detailů implementace a zobrazení pouze funkcionalit uživateli. Uživatel
   zná pouze to, co objekt dělá, ne jak to dělá.

2. **Dědičnost** - Dědičnost je mechanismus, který umožňuje vytvářet nové třídy z existujících tříd. Nová třída získává
   všechny metody a vlastnosti rodičovské třídy.

3. **Polymorfismus** - Polymorfismus umožňuje objektům vystupovat na mnoho různých způsobů. Například, můžeme mít
   třídu `Animal`, která má metodu `sound()`. Různé třídy zvířat mohou mít různé implementace této metody - kočka
   mňouká, pes štěká atd.

4. **Zapouzdření** - Zapouzdření znamená skrývání stavu objektu a jeho dat před ostatními objekty. Pouze metody objektu
   mohou manipulovat jeho stav.

## Agregace a kompozice

Agregace a kompozice jsou dva koncepty asociace, které jsou používány mezi třídami.

- **Agregace** - Agregace je slabší vztah. V agregaci je životnost obsažených objektů nezávislá na životnosti
  obsahujícího objektu. Například, pokud máme třídu `Car` a třídu `Wheel`, auto může existovat bez kola a kolo může
  existovat bez auta.

- **Kompozice** - Kompozice je silnější vztah. V kompozici je životnost obsažených objektů závislá na životnosti
  obsahujícího objektu. Například, pokud máme třídu `Human` a třídu `Heart`, srdce nemůže existovat bez člověka.

### Code example {id="code-example_1"}

```Java
class Wheel {
    // Wheel properties and methods
}

class Car {
    private Wheel wheel; // Car "has" a wheel - Aggregation

    public Car() {
        wheel = new Wheel();
    }
    // Car properties and methods
}

class Heart {
    // Heart properties and methods
}

class Human {
    private Heart heart; // Human "has" a heart - Composition

    public Human() {
        heart = new Heart();
    }
    // Human properties and methods
}