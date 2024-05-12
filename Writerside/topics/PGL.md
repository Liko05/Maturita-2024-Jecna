# 15. Programovací jazyky - vlastnosti, srovnání, popis způsobu tvorby i běhu programů

## Co je to programovací jazyk?

- Jazyk pro tvorbu programů. Programem máme na mysli sadu instrukcí pro počítač, jak vyřešit nějaký problém - algorithm.
- Každý jazyk má určité vlastnosti, které ho odlišují od ostatních jazyků.

## Nizší programovací jazyk

- Primitivní, nemají komplexní syntaxi, píšeme podobný způsob jako píšeme rovnou příkazy pro procesor.
- Procesor dělá určitou sadu instrukcí. Kód, který píšeme se nejdříve zpracuje do hexadecimálního kódu - strojový kód
  poté do binárního kódu. Binární informace jsou poté poslány do procesoru.

- **Příklad:** Assembler

## Vyšší programovací jazyk

- Více zkušeností programátora, znalost CPU, hardware.
- Díky tomu, že nepracujeme s primitivním kódem jako v nižších, můžeme dělat složitější akce. Počítač vlastně ani neví,
  co je for each. Proto kompilátor přeloží náš kód do instrukcí.

- **Příklad:** Java, C#, Python..

## Dělení dle kompilace

### Kompilované jazyky

- Příkladem je napřípad C,C++. Výsledkem jsou hexa soubory. Jsou rychlé.
- Pokud kód obsahuje chybu, kompilátor hodí chybu. Díky tomuto můžeme zjistit, kde je chyba před tím, než se začne
  spouštět kód.

### Interpretované jazyky

- Kompiluje jenom určité části kódu dle toho, jak je třeba.
- Příkladem je například Python, PHP. Python je pomalejší, ale je jednodušší na psaní.

- Výhodou je, že je přenositelný mezi platformami. Jde o to, že interpreter je tlumočník. Kód se přeloží do byte kódu,
  který je poté interpretován.
- Není potřeba dávat i datové typy, protože on je interpretuje postupně a můžou se měnit.

### Jazyky s VM

- Příkladem je Java. Vytváří bytecode. Řeší to problémy s hledáním chyb, ale je rychlejší než interpretované jazyky.

## Paradigmata

- Paradigma značí základní programovací styl.
- Dělí se na procedurální / imperatuvní a neproceduránlí / deklarativní.
- **Neprocedurální** jsou k tomu, abychom neřešili přesný postup, ale čeho má program dosáhnout.
- **Funkcionální** je program vytvořený z matematických funkcí.
- Logické, ten řeší pomocí matematiky a logických kroků.

## Dělení dle účelu

- Není jenom jeden jazyk, který by byl nejlepší. Každý jazyk má své výhody a nevýhody.

- **Web** - JavaScript, PHP, HTML, CSS
- **Desktop** - Java, C#, C++
- **Mobilní** - Java, Kotlin, Swift
- **Hry** - C++, C#, Java

## Statické a dynamické typování

- Statický je pevně definován datový typ při zakládání. Na začátku je jasné, jaký datový typ může proměnná mít a
  nemůžeme ho měnit.
- Dynamický je opak, datový typ je určen hodnotou proměnné. Hodnoty vznikají během programu a můžou se měnit.

## Syntaxe

- Syntaxe je způsob, jakým píšeme kód. Každý jazyk má svou syntaxi.
- Například u 🐍 se to řeší odsazení místo složených závorek při psaní kódu v bloku.