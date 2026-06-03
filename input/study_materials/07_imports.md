---
source: input/study_materials/07_imports.pdf
title: 07_imports
pages: 22
parsed_at: 2026-06-03T19:25:43.002Z
source_mtime: 2026-06-03T19:24:04.804Z
---

# 07_imports

## Strana 1

Import, balíčky
Václav Alt

## Strana 2

Import

## Strana 3

Import - Co je import?
Import je mechanismus v Pythonu, který zajišťuje následující
▶ překládá jméno na objekt modulu
▶ import foo.bar vede na objekt
▶ Modul se inicializuje pouze jednou
▶ Modul je dostupný pod zvoleným jménem uvnitř namespace
Vypadá jednoduše, ale je to komplexní proces.

## Strana 4

Import - Proč nás to zajímá
▶ Proč se modul spustí jen jednou
▶ Proč někdy musím restartovat kernel
▶ Proč circular importy dělají problémy
▶ Proč relativní cesty na soubory nefungují

## Strana 5

Import - Co je vlastně modul?
Z dřívějška
Modul je .py soubor, který můžeme importovat
Nyní
module = object + namespace
▶ module je objekt typu ModuleType
▶ obsahuje namespace ( __dict__ )
▶ import = vytvoření + naplnění namespace
Namespace - systém, ve kterém má každý objekt své unikátní jméno. V Pythonu má typicky
podobu slovníku

## Strana 6

Import - High-level struktura
Proces vyhodnocení import foo.bar lze konceptuálně rozdělit to následujících fází
1. Kontrola cache (sys.modules)
2. Nalezení specifikace modulu (finders)
3. Vytvoření objektu modulu
4. Načtení/spuštění modulu (loaders)
5. Svázání modulu se jménem

## Strana 7

Import - Přiřazení názvu
Potom, co je modul načten (loaded), proběhne name binding , tj.
1 import foo.bar
2 # vytvori:
3 foo = <module foo>
4 # foo.bar je dostupny jako atribut
Oproti tomu from foo import bar zpřístupní objekt bar z modulu foo a pojmenuje
jej (name binding) v lokální namespace:
Žádný nový modul se zde nevytváří, jde pouze o manipulaci se jmény.

## Strana 8

Import - 1. Kontrola cache
První krok je kontrola cache.
Cache sys.modules
Slovník ( dictionary ) mapující názvy modulů a již načtené objekty modulu
Pokud je foo.bar přítomen:
▶ Python ihned navrátí objekt modulu
▶ Žádná načítání z disku, žádné opětovné spouštění
▶ Díky tomu je načtený modul singleton (existuje pouze jedna instance)
▶ Top-level kód proběhne maximálně jednou
Cache modulů je klíčová pro
▶ výkon
▶ zamezení opakovaných side-effects
▶ průchod cyklickými importy

## Strana 9

Import - 2. Nalezení specifikace modulu
▶ Pokud modul není v sys.modules , Python se jej pokusí nalézt.
▶ K tomu slouží série finder objektů uložených v sys.meta_path
▶ Každý finder implementuje metodu find_spec(fullname, path,
target=None) a navrací specifikaci modulu ( ModuleSpec) , pokud ví, jak import
realizovat.
Výchozí import systém zahrnuje následující findery:
▶ Builtin finder: pro vestavěné moduly (sys, math)
▶ Frozen finder: pro frozen moduly (o tom jindy)
▶ Path-based finder (PathFinder): importy z filesystemu
PathFinder je pro běžné programování nejdůležitější:
▶ Prohledává lokace vypsané v sys.path
▶ u balíčků navíc lokace v __path__

## Strana 10

Import - Specifikace modulu (ModuleSpec)
Namísto přímého načtení modulu využívá Python meziobjekt ModuleSpec , který
obsahuje
▶ název modulu
▶ loader object
▶ tzv. origin (file path, aj.)
▶ informace o modulu/balíčku
▶ případně search paths pro submodul
Tím je odděleno kde modul žije od jak ho načíst

## Strana 11

Import - Path-based importy
Pro standardní importy PathFinder prohledá seznam sys.path
V něm najdeme
▶ current working directory (typicky odkud spouštíme interpreta nebo skript)
▶ installed packages
▶ standard library directories
Pro import balíku jako např. foo.bar
▶ foo je nalezen první
▶ foo.__path__ je použit k nalezení bar
Tenhle rekurzivní proces vystaví celou hierarchii modulů

## Strana 12

Import - 4. Načtení a spuštění modulu
Jakmile je nalezen objekt ModuleSpec , jeho loader je zodpovědný za
▶ vytvoření objektu modulu
▶ spuštění kódu v modulu
loader má typicky metody jako
▶ create_module(spec) - nepovinné, obvykle stačí default
▶ exec_module(module) - povinné

## Strana 13

Import - 4. Načtení a spuštění modulu
Creation phase
Objekt modulu je vytvořen, dostává atributy jako __name__ , __loader__ , __spec__
nebo __package__
Execution phase
Kód modulu je spuštěn ve vlastním namespace. To je ekvivalentní spuštění souboru
modulu standardně top-to-bottom.
V této fázi
▶ Jsou definovány všechny funkce a třídy modulu
▶ seběhne top-level kód
▶ seběhnou další importy v modulu

## Strana 14

Import - Bytecode a kompilace
▶ Při načítání .py souboru ho Python zkompiluje do bytecode.
▶ nasledné importy mohou tento cachovaný bytecode použít.
To odpovídá všeobecnému exekučnímu modelu v Pythonu:
source → AST → bytecode → execution in the interpreter loop

## Strana 15

Import - __name__ == "__main__"
▶ Každý modul má atribut __name__ .
▶ Při běžném importu dostane hodnotu skutečného jména modulu:
1 import mypkg.tool
2 # uvnitr modulu: __name__ == "mypkg.tool"
▶ Pokud je modul spuštěn jako vstupní bod programu, Python nastaví:
1 __name__ == "__main__"
▶ Proto konstrukce
1 if __name__ == "__main__":
2 main()
odděluje:
▶ kód určený pro import ,
▶ kód určený pro přímé spuštění .

## Strana 16

Import - python file.py vs. python -m package.module
▶
1 python file.py
spustí konkrétní soubor jako hlavní skript.
▶
1 python -m package.module
nejprve najde modul pomocí import machinery a pak jej spustí jako __main__ .
▶ Ve druhém případě Python zná balíčkový kontext modulu.
▶ To je důležité pro:
▶ relativní importy,
▶ korektní nastavení __package__ ,
▶ spouštění kódu uvnitř balíčků.

## Strana 17

Import - Proč python file.py někdy selže
▶ Uvažujme modul uvnitř balíčku:
1 # mypkg/tool.py
2 from . import utils
▶ Pokud spustíme:
1 python mypkg/tool.py
modul běží jako samostatný skript, nikoli jako součást balíčku.
▶ Python tedy nemá správně určený balíčkový kontext a relativní import může
skončit chybou:
1 ImportError: attempted relative import
2 with no known parent package
▶ Správné spuštění je:
1 python -m mypkg.tool

## Strana 18

Import - Absolutní vs. relativní import
▶ Import machinery vždy pracuje se jménem modulu .
▶ U absolutního importu je jméno zadané přímo:
1 from mypkg.core import parser
▶ U relativního importu se cílové jméno dopočítává z hodnoty __package__ .
▶ Například:
1 from . import utils
znamená přibližně: ”importuj utils ze stejného balíčku jako aktuální modul”.
▶ Pokud Python neví, do jakého balíčku aktuální modul patří, relativní import selže.
Důsledek: relativní importy jsou svázány s tím, jak byl modul spuštěn .

## Strana 19

Import - Vedlejší efekty importu
▶ Import není deklarace, ale vykonání modulu .
▶ Python při importu spustí top-level kód modulu.
▶ Proto mohou při importu nastat vedlejší efekty:
▶ tisk na obrazovku,
▶ otevření souboru,
▶ připojení k databázi,
▶ spuštění výpočtu,
▶ registrace handlerů či pluginů.
▶ Příklad:
1 print ("Loading configuration...")
2 config = load_config()
▶ Takový kód se provede už při samotném importu.

## Strana 20

Import - Lehké importy
▶ Dobrý modul by měl být při importu levný :
▶ bez dlouhých výpočtů,
▶ bez komunikace po síti,
▶ bez otevírání velkého množství souborů,
▶ bez silných vedlejších efektů.
▶ Import by měl hlavně:
▶ definovat funkce a třídy,
▶ nastavit konstanty,
▶ případně provést malou inicializaci.
▶ Těžší práci je vhodné přesunout:
▶ do funkcí,
▶ do metody main() ,
▶ nebo do explicitní inicializace.

## Strana 21

Import - Circular imports
▶ Moduly jsou někdy do sys.modules zapsány brzy a nemusí být ještě načteny.
▶ Kruhové importy tak nemusí vždy selhat, ale mohou vést k neúplně načtený
modulům, chybějícím atributům apod.
Příklad:
1 # a.py
2 import b
3 x = 1
1 # b.py
2 import a
3 print (a.x) # muze selhat
Zde a existuje v sys.modules , ale x ještě nemusí být definovaný

## Strana 22

Import - Vlastní importy
Tento import systém je rozšiřitelný
▶ Můžeme přidávat vlastní finders
▶ Můžeme definovat vlastní loader , které např. načtou module ze zip archivu,
nebot z databáze
Na základě toho lze vystavět například plugin system nebo rozličné pokročilé
frameworky
