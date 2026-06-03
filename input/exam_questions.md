---
source: input/exam_questions.pdf
title: exam_questions
pages: 6
parsed_at: 2026-06-03T19:54:23.726Z
source_mtime: 2026-06-03T19:49:18.542Z
---

# exam_questions

## Strana 1

Zkušební okruhy
BAPY
2026
Níže naleznete tematické okruhy, z nichž jeden dostanete u zkoušky. Každý okruh má několik podté-
mat, která byste v rámci své odpovědi měli pokrýt. Očekává se znalost zhruba v rozsahu probraném na
přednáškách a pokrytém v materiálech.

1. **Základní principy objektově orientovaného programování v Pythonu**
    - Vysvětlete pojmy třída, instance, atribut a metoda.
    - Rozlište atributy instance a atributy třídy.
    - Vysvětlete rozdíl mezi metodou instance, třídní metodou a statickou metodou.
    - Vysvětlete účel vybraných dunder metod.
    - Popište zapouzdření v Pythonu, privátní atributy, properties, gettery a settery.
    - Ukažte jednoduchý příklad třídy s vhodně navrženým rozhraním.
2. **Dědičnost v Pythonu**
    - Vysvětlete princip dědičnosti a vztah rodičovská třída – odvozená třída.
    - Vysvětlete vztah is-a a kdy je dědičnost vhodná.
    - Ukažte použití `super()`.
    - Vysvětlete překrývání metod.
    - Popište, jak se dědí atributy a metody.
    - Ukažte jednoduchý příklad dědičné hierarchie.
3. **Vícenásobná dědičnost, MRO a diamond problem**
    - Vysvětlete rozdíl mezi dědičností do hloubky a vícenásobnou dědičností.
    - Popište, co je MRO – Method Resolution Order.
    - Vysvětlete, proč záleží na pořadí rodičovských tříd.
    - Vysvětlete diamond problem / diamond of death.
    - Popište roli `super()` ve vícenásobné dědičnosti.
    - Ukažte, proč může být vícenásobná dědičnost zdrojem nepřehledného návrhu.
4. **Abstraktní třídy, typy a kompozice jako alternativa k dědičnosti**
    - Vysvětlete, co je abstraktní třída a k čemu slouží.
    - Popište použití `ABC` a `@abstractmethod`.
    - Vysvětlete rozdíl mezi `type`, `isinstance` a `issubclass`.
    - Vysvětlete, kdy je vhodnější použít kompozici místo dědičnosti.
    - Vysvětlete pojem mixin a uveďte jeho typické použití.
    - Diskutujte rizika příliš složitých dědičných hierarchií.

## Strana 2

5. **Polymorfismus a duck typing**
    - Vysvětlete obecnou myšlenku polymorfismu.
    - Vysvětlete princip “stejné volání, různé chování”.
    - Popište duck typing v Pythonu.
    - Vysvětlete pojem implicitní kontrakt.
    - Uveďte výhody a nevýhody duck typingu.
    - Ukažte příklad funkce, která pracuje polymorfně bez dědičnosti.
6. **Subtypový polymorfismus, rozhraní a protokoly**
    - Vysvětlete subtypový polymorfismus.
    - Popište, jak souvisí subtypový polymorfismus s dědičností.
    - Vysvětlete rozdíl mezi nominálním a strukturálním typováním.
    - Popište použití `Protocol`.
    - Porovnejte `ABC` a `Protocol`.
7. **Iterátory a formy polymorfismu**
    - Vysvětlete, co znamená, že objekt je iterovatelný.
    - Popište vztah mezi iterovatelným objektem a iterátorem.
    - Vysvětlete použití `iter`, `next` a `StopIteration`.
    - Uveďte příklad vlastní implementace iterátoru.
    - Vysvětlete rozdíl mezi ad-hoc, subtypovým a parametrickým polymorfismem.
    - Vysvětlete, jak souvisí generika s parametrickým polymorfismem.
8. **Základní UML vztahy**
    - Vysvětlete, k čemu slouží UML v návrhu programu.
    - Popište UML reprezentaci třídy, atributů a metod.
    - Vysvětlete dědičnost a implementaci rozhraní v UML.
    - Vysvětlete asociaci, agregaci a kompozici.
    - Nakreslete nebo popište jednoduchý UML diagram pro několik spolupracujících tříd.
9. **Návrhové vzory a jejich role v návrhu programu**
    - Vysvětlete, co je návrhový vzor.
    - Vysvětlete, proč návrhový vzor není hotový kus kódu.
    - Popište, jak návrhové vzory souvisí s OOP, dědičností a polymorfismem.
    - Vysvětlete, jak programovací jazyk ovlivňuje podobu návrhového vzoru.
    - Uveďte příklad situace, kdy je návrhový vzor užitečný.
    - Uveďte riziko přehnaného používání návrhových vzorů.
10. **Návrhový vzor Adapter**
    - Vysvětlete problém, který Adapter řeší.
    - Popište role Client, Target interface, Adapter a Adaptee.
    - Vysvětlete, proč nechceme nebo nemůžeme měnit původní implementaci.
    - Popište typické použití
    - Ukažte jednoduchý příklad adapteru v Pythonu.

## Strana 3

    - Vysvětlete, jak Adapter souvisí s polymorfismem a rozhraním.
11. **Návrhové vzory Strategy a Observer**
    - Vysvětlete princip návrhového vzoru Strategy.
    - Popište, jak Strategy odděluje algoritmus od objektu, který ho používá.
    - Vysvětlete, proč Strategy často používá kompozici místo dědičnosti.
    - Vysvětlete princip návrhového vzoru Observer.
    - Popište role Subject / Publisher a Observer / Subscriber.
    - Uveďte příklad, kde se hodí Strategy, a příklad, kde se hodí Observer.
12. **Decorator jako návrhový vzor a dekorátory v Pythonu**
    - Vysvětlete princip wrapperu.
    - Popište návrhový vzor Decorator jako rozšíření chování bez úpravy původního objektu.
    - Vysvětlete rozdíl mezi Decorator pattern a syntaxí @decorator v Pythonu.
    - Popište, jak funguje dekorátor funkce.
    - Vysvětlete souvislost mezi dekorátory, memoizací a `lru_cache`.
13. **Paměť počítače, stack a heap**
    - Vysvětlete paměť počítače jako adresovatelnou oblast bytů.
    - Popište vztah proměnných a paměti.
    - Vysvětlete, co je stack a stack frame.
    - Popište, jak souvisí stack s voláním funkcí.
    - Vysvětlete, co je heap a dynamická alokace.
    - Porovnejte vlastnosti stacku a heapu.
14. **Ruční a automatická správa paměti**
    - Vysvětlete ruční správu paměti na příkladu jazyka C.
    - Popište význam `malloc` a `free`.
    - Vysvětlete chyby memory leak, dangling pointer a segmentation fault.
    - Vysvětlete pojem undefined behavior.
    - Popište základní myšlenku automatické správy paměti.
    - Porovnejte reference counting a garbage collection.
15. **Správa paměti a proměnné v Pythonu**
    - Vysvětlete, co znamená, že proměnná v Pythonu je jméno navázané na objekt.
    - Popište sdílení objektů více jmény.
    - Vysvětlete, co přesně dělá příkaz `del`.
    - Vysvětlete životnost objektu podle existence referencí.
    - Popište reference counting v CPythonu.
    - Vysvětlete problém referenčních cyklů a roli garbage collectoru.
16. **Numpy**
    - Vysvětlete, proč jsou explicitní Python cykly pomalé pro velká numerická data.
    - Popište základní myšlenku práce s celými poli najednou.

## Strana 4

    - Vysvětlete, co je `ndarray` a jeho vlastnosti `shape`, `dtype`, `ndim` a `size`.
    - Popište základní indexování NumPy polí.
    - Vysvětlete pojem vektorizace.
    - Vysvětlete rozdíl mezi vektorizovaným výpočtem a explicitním Python cyklem.
    - Uveďte příklad výpočtu, který lze výrazně zjednodušit pomocí NumPy.
17. **Základy práce s daty v Pandas**
    - Představce balík Pandas.
    - Vysvětlete, co je `Series`.
    - Popište roli indexu.
    - Vysvětlete, co je `DataFrame`.
    - Popište práci se sloupci a řádky.
    - Ukažte základní výběr dat.
    - Popište základní exploraci dat v Pandas.
18. **Základy vizualizace dat pomocí Matplotlib**
    - Vysvětlete základní princip kreslení grafů v Matplotlib.
    - Popište vztah figure a axes.
    - Vysvětlete význam popisků, legendy a velikosti grafu.
    - Popište použití colormap.
    - Vysvětlete použití sloupcového grafu.
19. **Import v Pythonu**
    - Popište modul jako objekt a namespace.
    - Popište základní fáze importu: cache, finders, `ModuleSpec`, loaders, vytvoření modulu, spuštění kódu, name binding.
    - Vysvětlete roli `sys.modules` a proč se top-level kód modulu nespouští při každém importu znovu.
    - Popište, co dělá `PathFinder` a vysvětlete význam `sys.path`.
    - Porovnejte spuštění `python file.py` a `python -m package.module`.
    - Vysvětlete absolutní a relativní importy.
20. **Rekurze, iterace, memoizace a dynamické programování**
    - Vysvětlete princip rekurze.
    - Popište base case a rekurzivní krok.
    - Vysvětlete časovou a paměťovou náročnost rekurzivního řešení.
    - Rozlište head a tail rekurzi.
    - Vysvětlete memoizaci a cache mezivýsledků.
    - Popište použití `functools.lru_cache`.
    - Porovnejte rekurzi a iteraci jako dva způsoby řízení výpočtu.
21. **Lazy evaluation, generátory a yield**
    - Vysvětlete princip lazy evaluation.
    - Porovnejte list comprehension a generator expression.
    - Vysvětlete, co je generátor.

## Strana 5

    - Popište, co dělá `yield`.
    - Vysvětlete, jak se při generování zachovávají lokální proměnné a pozice v kódu.
    - Uveďte příklad, kdy je generátor vhodnější než seznam.
22. **Higher-order funkce, closure a lambda funkce**
    - Vysvětlete, co znamená, že funkce jsou v Pythonu objekty.
    - Popište funkce jako argumenty.
    - Popište funkce jako návratové hodnoty.
    - Vysvětlete pojem higher-order function.
    - Vysvětlete closure jako funkci se zachyceným prostředím.
    - Uveďte příklad closure.
    - Vysvětlete roli lambda funkcí.
23. **Unit testy a testovatelný kód**
    - Vysvětlete rozdíl mezi unit testy, integračními testy a end-to-end testy.
    - Vysvětlete motivaci unit testů.
    - Popište, jak testy dokumentují očekávané chování.
    - Vysvětlete, co znamená testovatelný kód.
    - Popište čisté funkce a omezení side effects.
    - Vysvětlete dependency injection.
    - Vysvětlete oddělení výpočtu od vstupu/výstupu, UI, souborového systému nebo sítě a souvislost s testováním.
24. **Modul unittest, mocking, patching a TDD**
    - Popište základní strukturu testu pomocí `unittest`.
    - Vysvětlete `TestCase`, testovací metody a assertions.
    - Vysvětlete test discovery a organizaci testů v projektu.
    - Popište účel `setUp` a `tearDown`.
    - Vysvětlete princip mockingu a patchingu.
    - Vysvětlete základní myšlenku test-driven development.
    - Popište cyklus red-green-refactor.
25. **Uživatelská rozhraní a obecná struktura interaktivního programu**
    - Vysvětlete pojem uživatelské rozhraní.
    - Porovnejte jednorázový skript a interaktivní program.
    - Popište obecnou strukturu interaktivního programu.
    - Vysvětlete pojmy hlavní smyčka, událost, obsluha události a stav programu.
    - Uveďte příklady událostí v programu.
26. **CLI, argparse a automatizace**
    - Vysvětlete, co je command line interface.
    - Popište poziční argumenty, volitelné argumenty a přepínače.
    - Vysvětlete zásady návrhu dobrého CLI.
    - Popište použití modulu `argparse`.

## Strana 6

    - Vysvětlete, proč je CLI vhodné pro automatizaci.
    - Vysvětlete rozdíl mezi CLI, TUI a GUI.
    - Vysvětlete účel modulu `cmd`.
    - Popište základní pojmy GUI: widget, layout, callback.
    - Vysvětlete princip `mainloop` v GUI aplikaci.
27. **Základní koncepty architektury**
    - Popište princip *separation of concerns*.
    - Vysvětlete pojmy *cohesion* a *coupling*.
    - Vysvětlete rozdíl mezi běžným výstupem programu a diagnostickým výstupem.
    - Vysvětlete, kdy použít `print` a kdy logging, popište základní úrovně loggingu a jejich význam.
    - Vysvětlete MVC architekturu.
    - Vysvětlete princip dependency injection na jednoduchém příkladu.
28. **Serializace dat a objektů v Pythonu**
    - Vysvětlete, co je serializace a deserializace.
    - Vysvětlete, jaké problémy mohou vzniknout při ukládání objektů.
    - Uveďte, jaké typy lze do JSONu ukládat přímo a jaká omezení JSON má.
    - Vysvětlete, jak může při serializaci pomoci `dataclass`.
    - Vysvětlete, k čemu slouží modul `pickle`, jaké jsou výhody a nevýhody.
    - Vysvětlete bezpečnostní problém deserializace pomocí `pickle`.
