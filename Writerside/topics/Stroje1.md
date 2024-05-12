# 17. Strojové učení - Příprava dat, Chyby v datech a bias, Korelace a kauzalita

## Co je strojové učení?

- Je obor umělé inteligence, který se zabývá vývojem algoritmů, které se učí na základě dat.
- Algorimy umožňují počítačům automaticky se učit a zlepšovat svou výkonnost.
- Místo přímeho programování jednotlivých kroků algoritmu, se programu poskytnou data a výstup, který se má dosáhnout.

### Příklad strojového učení

- Například máme na vstupu obrázek psa a program má určit, zda se na obrázku nachází pes nebo něco jiného.
- Dalším příkladem může být v nějakém jazyce textový řetězec a program má přeložit text do jiného jazyka.

## Strojové učení

- Strojové učení se opírá o matematické a statistické metody, které umožňují počítači se učit na základě dat.
- Z těchto dat si můžeme udělat model, který nám umožní predikovat výsledky na základě nových dat.
- Tato data mohou být **struktorována**, tabulky s hodnotami, nebo **nestruktována**, text,obázek...
- Algoritmy strojového učení se pak snaží nalézt vzory a vztahy v datech a tyto vzory použít ke zlepešní
- Existuje několik přístupů učení, včetne supervizovaného, kdy jsou modely trénovány na datech s předem známými výstupy.
  Nesupervizované učení, které se zaměřuje na objevování vzorců a struktur v datech
    - **Učení s učitelem** - Supervised learning
    - **Učení bez učitele** - Unsupervised learning

## Příprava dat

- Je to proces, ve kterém se data upravují, transformují a čístí, aby byla vhodná pro analýzu a strojové učení.
- Tento proces zahrnuje odstranění chybějících hodnot, normalizaci dat, vyřešení odlehlých hodnot a další...
- P5íprava dat je velice důležitá, protože špatně připravená data mohou vést k špatným výsledkům a zkresleným modelům.

## Chyby v datech a bias

- Chyby v datech se mohou objevit z různých důvodů, například kvůli lidské chybě při sběru dat, technickým problémům
  nebo nesprávně interpretaci.
- Důležité je identifikovat a řešit tyto chyby, protože mohou ovlivnit validitu a spolehlivost vašich výsledků

### Bias

- Bias v datech se týká situace, kdy jso udata záměrně nebo neúmyslně ovlivněna určitým směrem
- Například pokud je dataset pouze s určitou skupinou lidí a zanedbáme ostatní, může to vést k zkresleným výsledkům.

## Korelace a kauzalita

### Korelace

- Vztahuje se k míře, kterou dvě proměnné souvisí mezi sebou.
- Pokud mají silnou korelaci, znamená to, že jejich se hodnoty často mění ve stejném směru
- Nelze říci, že změna jedné proměnné způsobí změnu druhé proměnné

### Kauzalita

- Vzah příčiny a následku mezi dvěma proměnnými.
- Prokázat souvislost mezi dvěma proměnnými vyžaduje další analýzu a experimenty.
- Strojové učení se obecně zaměřuje na predikci a korelace mezi proměnnými
