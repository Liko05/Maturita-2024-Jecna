# 21. Typy datových struktur - Pole, Spojový seznam, Strom, Fronta, Zásobník, Halda

- Datové struktury jsou základním pojmem v programování, jak jsou data uložena v paměti počítače
- Základními datovými strukturami jsou pole, spojový seznam, strom, fronta, zásobník a haldy

## Pole

- Pole je datová struktura, která umožňuje ukládání více prvků stejného typu za sebou v paměti.
- Prvky pole jsou indexovány od nuly.
- Automaticky alokuje paměť pro všechny prvky pole, což znamená, že prvky lze přidat, odebrat či přesouvat za běhu programu

**Příklad pole:**

```Java
int[] pole = new int[5];
pole[0] = 1;
pole[1] = 2;
```

## Spojový seznam

- Spojový seznam je dynamická datová struktura, která umožnuje ukládání prvků v hierarchické struktuře.
`Hierarchická struktura` znamená, že každý prvek seznamu obsahuje odkaz na další prvek.
- Každý prvek spojového seznamu se nazývá `Node`.
- Spojový seznam může být jednosměrný nebo obousměrný.
- Jednosměrný spojový seznam má každý uzel odkaz na následující uzel.
- Obousměrný spojový seznam má každý uzel odkaz na následující i předchozí uzel.

**Příklad jednosměrného spojového seznamu:**

```Java
class Node {
    int hodnota;
    Node dalsi;
}

Node prvni = new Node();
prvni.hodnota = 1;
prvni.dalsi = new Node();
prvni.dalsi.hodnota = 2;
```

**Příklad obousměrného spojového seznamu:**

```Java
class Node {
    int hodnota;
    Node dalsi;
    Node predchozi;
}

Node prvni = new Node();
prvni.hodnota = 1;
prvni.dalsi = new Node();
prvni.dalsi.hodnota = 2;
prvni.dalsi.predchozi = prvni;
```

## Strom

- Strom je hierarchická datová struktura, která umožňuje ukládání prvků v hierarchické struktuře.
- Každý prvek stromu má jednoho rodiče a několik potomků.

**Příklad stromu:**

```Java
class Node {
    int hodnota;
    List<Node> potomci;
}

Node koren = new Node();
koren.hodnota = 1;
koren.potomci = new ArrayList<>();
koren.potomci.add(new Node());
koren.potomci.get(0).hodnota = 2;
```

## Fronta

- Fronta (FIFO) je datová struktura, která umožňuje ukládání prvků a jejich zpracování v pořadí, ve kterém byly přidány.
- Operace s frontou jsou `add` (vložení prvku na konec fronty) a `poll` (odebrání prvního prvku z fronty).

**Příklad fronty:**

```Java
Queue<Integer> fronta = new LinkedList<>();
fronta.add(1);
fronta.add(2);
int prvni = fronta.poll();
```

## Zásobník

- Zásobník (LIFO) je datová struktura, která umožňuje ukládání prvků a jejich zpracování v opačném pořadí, ve kterém byly přidány.
- Operace se zásobníkem jsou `push` (vložení prvku na vrchol zásobníku) a `pop` (odebrání prvku z vrcholu zásobníku).

**Příklad zásobníku:**

```Java
Stack<Integer> zasobnik = new Stack<>();
zasobnik.push(1);
zasobnik.push(2);
int vrchol = zasobnik.pop();
```

## Halda

- Halda je datová struktura, která umožňuje ukládání prvků a jejich zpracování v pořadí podle priorit.
- Rozlišujeme `min-heap` a `max-heap`
- Min-heap - hodnota každého uzlu je menší nebo rovna jeho potomků
- Max-heap - hodnota každého uzlu je větší nebo rovna jeho potomků
- Operace s haldou jsou `add` (vložení prvku do haldy) a `poll` (odebrání prvku z haldy s nejvyšší prioritou).

**Příklad haldy:**

```Java
PriorityQueue<Integer> halda = new PriorityQueue<>();
halda.add(1);
halda.add(2);
int nejvyssiPriorita = halda.poll();
```
