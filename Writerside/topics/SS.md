# 16. Soubory a serializace - Ukládání a načítání dat, formáty souborů

## Serializace

- Serializace je proces, převod objektů nebo datových struktur do formátu, který bude jednoduše přenositelný.
- Používá se například pro ukládání stavu aplikace, ukládání a načtení konfiguračních souborů nebo obyčejný přenos dat
  mezi procesy v počítači.
- Během serializace jsou data přenášena jako série bytů, které se následně zase deserializují do původní podoby.

## Soubory

- Soubor je pojmenovaná skupina nějakých dat.
- Data můžou být různého typu. Soubory se používají k organizaci dat a mohou být jakkoliv upravovány, čteny a posílány.
- Pro práci v Javě můžeme použít
  třídy `File`, `FileInputStream`, `FileOutputStream`, `BufferedReader`, `BufferedWriter`, `PrintWriter` a další.

## Serializování objektů

- Používáme třídu `Serializable`
- Serializujeme celý objekt, můžeme to ale obejít tím, že použijeme `transient` klíčové slovo.
- Pro serializování objektů se používá třída `ObjectOutputStream`.
- Důležité je mít také `FileOutputStream` - vytvoří Stream a ObjectOutputStream tento výstupní Stream zabalí tak, aby se
  vědělo že se jedná o serializovaný objekt.

## Deserializace

- Deserializace je proces, kdy se série bytů převede zpět na objekt.
- Pro deserializaci objektů se používá třída `ObjectInputStream`.
- Důležité je mít také `FileInputStream` - vytvoří Stream a ObjectInputStream tento vstupní Stream zabalí tak, aby se
  vědělo že se jedná o serializovaný objekt.

## Formáty souboru

- Soubory mohou být různých formátů, například textové, binární, XML, JSON, CSV, YAML, ...
- Formát nám říka, co můžeme v souboru očekávat a jak s ním pracovat.

### Textové soubory

- Textové soubory obsahují textová data.
- Jsou čitelné pro člověka i pro stroj.
- Příkladem může být soubor s konfigurací, logovací soubor, zdrojový kód, ...

### Binární soubory

- Binární soubory obsahují binární data.
- Nejsou čitelné lidmi, jsou skládány do nějakého formátu pro účely kompilace nebo interpretace.
- Příkladem může být právě serializovaný objekt.