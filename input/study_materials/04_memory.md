---
source: input/study_materials/04_memory.pdf
title: 04_memory
pages: 50
parsed_at: 2026-06-03T19:25:42.939Z
source_mtime: 2026-06-03T19:24:04.813Z
---

# 04_memory

## Strana 1

Správa paměti, data model, GC
Václav Alt

## Strana 2

Motivace: Co je paměť

## Strana 3

Motivace: Co je paměť - Paměť počítače
Program během běhu pracuje s pamětí. Paměť si lze představit jako velké pole bytů,
kde každý byte má svou adresu.
Adresa Obsah
0x1000 42
0x1001 00
0x1002 A3
0x1003 17
Procesor provádí instrukce, které:
▶ čtou data z paměti
▶ zapisují data do paměti
▶ pracují s adresami
Proměnné v programu tedy v konečném důsledku odpovídají nějakým oblastem paměti.

## Strana 4

Motivace: Co je paměť - Správa paměti
Programy potřebují paměť během běhu:
▶ ukládání proměnných
▶ vytváření datových struktur
▶ ukládání mezivýsledků výpočtu
Otázky, které musí jazyk nebo runtime řešit:
▶ Kde se paměť přidělí?
▶ Jak dlouho bude existovat?
▶ Kdy se uvolní?
Tomu říkáme správa paměti .

## Strana 5

Stack a heap

## Strana 6

Stack a heap - Základní oblasti paměti
Ve většině programů se používají dvě hlavní oblasti paměti:
▶ Stack (zásobník)
▶ Heap (halda)
Tyto oblasti mají odlišné vlastnosti a používají se pro různé typy dat.
Rozdíl mezi stackem a heapem je zásadní pro pochopení chování programů.

## Strana 7

Stack a heap - Stack
Stack je paměť používaná především pro volání funkcí.
Každé volání funkce vytvoří tzv. stack frame , který obsahuje:
▶ lokální proměnné
▶ parametry funkce
▶ návratovou adresu
Příklad v jazyce C:
1 void foo() {
2 int x = 10;
3 int y = 20;
4 }
Po zavolání funkce se proměnné uloží na stack. Po návratu z funkce se celý rámec
odstraní.

## Strana 8

Stack a heap - Vlastnosti stacku
Stack funguje jako zásobník - datová struktura typu LIFO - last in, first out.
▶ velmi rychlá alokace
▶ paměť se uvolňuje automaticky
▶ omezená velikost
Každé nové volání funkce přidá další rámec na stack.

## Strana 9

Stack a heap - Stack overflow
▶ Stack má omezenou velikost.
▶ Pokud program vytváří příliš mnoho rámců, může dojít k přetečení zásobníku.
▶ Typický příklad je nekonečná rekurze:
1 void f() {
2 f();
3 }
▶ Každé volání přidá nový rámec na stack, dokud paměť nedojde.
▶ Výsledkem je stack overflow .

## Strana 10

Heap a dynamická alokace

## Strana 11

Heap a dynamická alokace - Heap
▶ Heap je oblast paměti určená pro dynamickou alokaci.
▶ Paměť se přiděluje za běhu programu podle potřeby.
V jazyce C:
1 int *p = malloc( sizeof ( int ));
2 *p = 10;
3 free(p);
Paměť zůstává alokovaná, dokud ji program explicitně neuvolní.

## Strana 12

Heap a dynamická alokace - Stack vs Heap
Stack Heap
automatická správa ruční správa
rychlá alokace pomalejší alokace
malá velikost velká velikost
lokální proměnné dynamické struktury
Stack je vhodný pro krátkodobá data.
Heap se používá pro:
▶ velké struktury
▶ objekty s neznámou životností
▶ dynamická data

## Strana 13

Problémy manuální správy

## Strana 14

Problémy manuální správy - Pointery v C
V jazyce C může proměnná obsahovat adresu paměti . Taková proměnná se nazývá
ukazatel (pointer).
1 int x = 10;
2 int *p = &x;
3
4 printf("%d\n", *p);
Význam:
▶ &x získá adresu proměnné
▶ p ukládá tuto adresu
▶ *p dereferencuje ukazatel

## Strana 15

Programátor tak může pracovat přímo s adresami v paměti.
Výhoda:
▶ velmi přesná kontrola nad pamětí
Nevýhoda:
▶ velmi snadno vznikají chyby
Proto jazyky jako Python ukazatele běžně nepoužívají.
Nejčastější chyby:
▶ Memory leak
▶ Dangling pointer
▶ Segmentation fault

## Strana 16

Problémy manuální správy - Memory leak
Memory leak nastává, když program alokuje paměť, ale nikdy ji neuvolní.
1 int *p = malloc( sizeof ( int ));
Pokud se nikdy neprovede
1 free(p);
paměť zůstane rezervovaná až do ukončení programu.
Důsledky:
▶ postupné zvětšování spotřeby paměti
▶ zpomalení programu
▶ případný pád aplikace

## Strana 17

Problémy manuální správy - Dangling pointer
Dangling pointer je ukazatel na paměť, která již byla uvolněna.
1 int *p = malloc( sizeof ( int ));
2 free(p);
3
4 *p = 10; // chyba
Program zapisuje do paměti, která už nepatří programu.
Výsledek je undefined behavior . Což nastává v situacích, kdy programovací jazyk nijak
nedefinuje, co se má stát. Program může spadnou, fungovat náhodně nebo zdánlivě
správně.

## Strana 18

Problémy manuální správy - Segmentation fault
Segmentation fault (často segfault) nastane při přístupu do nepovolené oblasti paměti.
Například přístup mimo pole nebo dereference NULL
1 int a[3];
2 a[10] = 5;
nebo dereference neplatného ukazatele:
1 int *p = NULL;
2 *p = 10;
Operační systém detekuje přístup do nepovolené paměti a proces ukončí signálem
(typicky SIGSEGV)

## Strana 19

Problémy manuální správy - Proč to vůbec řešíme?
Ruční správa paměti (např. v C):
▶ je rychlá
▶ dává velkou kontrolu
▶ náchylná k chybám
Z toho důvodu řada moderních jazyků používá automatickou správu paměti .

## Strana 20

Automatická správa

## Strana 21

V některých jazycích probíhá automatická správa paměti – nemá ji na starosti
programátor, ale kompilátor/interpret/runtime environment.
Mezi nejběžnější techniky automatické správy paměti patří
▶ Reference counting
▶ Garbage collection
▶ Region/Arena
▶ Ownership

## Strana 22

Automatická správa - Správa paměti v různých jazycích
Různé programovací jazyky používají různé strategie.
Jazyk Správa paměti
C manuální (malloc / free)
C++ převážně manuální + RAII
Rust ownership systém
Java garbage collector
C# garbage collector
Go garbage collector
Python reference counting + GC
Trendy moderních jazyků:
▶ minimalizovat manuální správu paměti
▶ snížit počet chyb
▶ zachovat přijatelný výkon

## Strana 23

Automatická správa - Správa paměti v Pythonu
Python skrývá většinu detailů správy paměti.
Programátor obvykle:
▶ nepoužívá ukazatele
▶ nepřiděluje paměť ručně
▶ paměť neuvolňuje explicitně
Paměť spravuje runtime Pythonu pomocí:
▶ reference counting
▶ garbage collection

## Strana 24

Python runtime

## Strana 25

Python runtime - Python Virtual Machine
▶ Python je interpretovaný jazyk – to je pravda jen částečně
▶ zdrojový kód v Pythonu je nejprve přeložen do bytecode – sady jednoduchých
instrukcí
▶ Samotný chod programu v Python zajišťuje Python Virtual Machine (PVM)
▶ PVM bere jednotlivé bytecode instrukce a postupně je vykonává
▶ Proto Python není čistě interpretovaný jazyk.

## Strana 26

Python runtime - Implementace Pythonu
Python není jeden konkrétní program.
Je to programovací jazyk , který může mít více implementací.
Nejznámější:
▶ CPython
▶ referenční implementace
▶ napsaná v jazyce C
▶ používá reference counting
▶ PyPy
▶ implementace v Pythonu (RPython)
▶ obsahuje JIT kompilátor
▶ Jython
▶ běží nad Java Virtual Machine
▶ IronPython
▶ běží nad .NET
▶ MicroPython
▶ Python pro mikrokontroléry
Ve většině případů když říkáme „Python“, myslíme CPython.

## Strana 27

Python runtime - Jazyk vs implementace
Je důležité rozlišovat:
Vlastnosti jazyka
▶ syntaxe
▶ typový systém
▶ objektový model
Ty jsou stejné pro všechny implementace.
Vlastnosti implementace
▶ způsob správy paměti
▶ rychlost programu
▶ zda se používá JIT kompilace
▶ interní reprezentace objektů
Například:
▶ CPython používá reference counting
▶ jiná implementace může používat pouze garbage collector
Program by ale měl fungovat stejně.

## Strana 28

Proměnné v C a Pythonu

## Strana 29

Proměnné v C a Pythonu - Proměnná v jazyce C
V jazyce C je proměnná přímo oblast paměti.
1 int x = 10;
Paměť může vypadat například takto:
Adresa Hodnota
1000 10
▶ Proměnná tedy reprezentuje konkrétní byty v paměti.
▶ Deklarace int x = 10; tedy říká něco ve smyslu: tamhle v paměti (na adrese
pod názvem x ) je několik bytů (typicky 4), do kterých zapisujeme celé číslo

## Strana 30

Proměnné v C a Pythonu - Proměnná v Pythonu
V Pythonu je proměnná pouze jméno odkazující na objekt.
1 x = 10
Schéma:
x → objekt typu int
Objekt obsahuje:
▶ typ
▶ hodnotu
▶ další metadata
Objekt int v Pythonu je mnohem složitější věc než několik bytů s číslem

## Strana 31

Proměnné v C a Pythonu - Sdílení objektů
Více proměnných může odkazovat (referovat) na stejný objekt.
1 a = [1,2,3]
2 b = a
Obě jména ukazují na stejný seznam.
1 b.append(4)
2 print (a)
Výsledek (protože seznam je mutable):
1 [1,2,3,4]

## Strana 32

Reference counting

## Strana 33

Reference counting - Reference counting
▶ Python používá mechanismus zvaný reference counting - počítání referencí.
▶ Každý objekt si pamatuje počet referencí, které na něj existují.
▶ Reference counting je implementační detail CPythonu.
▶ Reference counting vyřeší většinu případů (na zbytek garbage collector)
1 a = [1,2]
2 b = a
Počet referencí na objekt je nyní 2.
Pokud reference zmizí:
1 b = None
počítadlo se sníží.

## Strana 34

Reference counting - Zánik objektu
Když počet referencí klesne na nulu, objekt se odstraní z paměti.
1 a = [1,2]
2 b = a
3
4 a = None
5 b = None
▶ Seznam již nemá žádné reference a může být uvolněn.
▶ Výhodou je, že objekt může být uvolněn velmi brzy po ztrátě poslední reference
(typicky okamžitě v CPythonu)

## Strana 35

Reference counting - Reference counting v praxi
V modulu sys lze orientačně zjistit počet referencí na objekt pomocí
sys.getrefcount() .
1 import sys
2
3 a = []
4 print (sys.getrefcount(a))
Typicky se vypíše 2 , což bývá na první pohled překvapivé.
Důvod je ten, že:
▶ jedna reference je uložená v proměnné a
▶ druhá reference vznikne při předání objektu jako argument do funkce
getrefcount
Proto je třeba výsledek chápat opatrně: getrefcount(obj) ukazuje o jednu referenci
více, než bychom intuitivně čekali.

## Strana 36

Reference counting - Co dělá del
Příkaz del nemaže přímo objekt. Maže jméno, tedy jednu referenci.
1 import sys
2
3 a = [1, 2, 3]
4 b = a
5
6 print (sys.getrefcount(a)) # typicky 3
7
8 del b
9 print (sys.getrefcount(a)) # typicky 2
Interpretace:
▶ nejprve existují dvě běžné reference: a a b
▶ volání getrefcount(a) přidá dočasně ještě jednu
▶ po del b zůstává už jen jméno a
Kdybychom nakonec provedli i
1 del a
objekt by už neměl žádnou běžnou referenci a v CPythonu by typicky hned zanikl.

## Strana 37

Reference counting - Referenční cyklus
Samotné reference counting nestačí, po-
kud objekty odkazují jeden na druhý.
1 import sys
2
3 a = []
4 b = []
5
6 a.append(b)
7 b.append(a)
8
9 print (sys.getrefcount(a))
10 print (sys.getrefcount(b))
Schéma situace:
▶ a odkazuje na seznam b
▶ b odkazuje na seznam a
I kdybychom pak smazali jména
1 del a
2 del b
▶ objekty na sebe stále odkazují.
▶ Jejich reference count tedy neklesne
na nulu jen pomocí tohoto
mechanismu.
▶ Takové objekty musí později najít
garbage collector.

## Strana 38

Garbage collector

## Strana 39

Garbage collector - Problém cyklů
▶ Reference counting má jeden problém.
▶ Objekty mohou vytvářet cykly.
1 a = []
2 b = []
3
4 a.append(b)
5 b.append(a)
Objekty na sebe odkazují, takže jejich reference count neklesne na nulu.

## Strana 40

Garbage collector - Generační garbage collector
Python používá doplňkový garbage collector, který hledá cykly.
Objekty jsou rozděleny do generací:
▶ generace 0 – nové objekty
▶ generace 1
▶ generace 2 – dlouho žijící objekty
Myšlenka: většina objektů zanikne velmi rychle.
Garbage collector proto kontroluje mladší generace častěji.

## Strana 41

Garbage collector - Prahy garbage collectoru
Modul gc umožňuje zjistit aktuální nastavení spouštění garbage collectoru.
1 import gc
2
3 print (gc.get_threshold())
4 print (gc.get_count())
Typický význam:
▶ get_threshold() vrací prahy, podle nichž se collector spouští
▶ get_count() vrací aktuální počítadla od posledních sběrů
Prahy lze změnit:
1 import gc
2
3 print (gc.get_threshold())
4
5 gc.set_threshold(700, 10, 10)
6 print (gc.get_threshold())

## Strana 42

Garbage collector - Ruční spuštění collectoru
Garbage collector lze spustit i ručně.
1 import gc
2
3 n = gc.collect()
4 print (n)
Hodnota n udává, kolik objektů bylo při daném průchodu nalezeno jako odstranitelné
nebo neodstranitelné.
Lze požádat i o konkrétní úroveň sběru:
1 import gc
2
3 gc.collect(0) # mladé objekty
4 gc.collect() # plný ě sbr

## Strana 43

Garbage collector - Kdy gc.collect() používat
V běžném Python kódu se gc.collect() obvykle nevolá ručně.
Typické rozumné situace jsou:
▶ demonstrace chování garbage collectoru ve výuce
▶ ladění podezřelých cyklů a úniků paměti
▶ měření, kdy chceme před experimentem “uklidit” stav
▶ speciální dlouho běžící programy, kde dobře víme, proč to děláme
Ukázka ladicího použití:
1 import gc
2
3 gc.set_debug(gc.DEBUG_LEAK)
4 gc.collect()
Naopak není dobrý nápad volat gc.collect() po každé funkci nebo v každé smyčce.
Ve většině případů je lepší nechat collector pracovat automaticky.

## Strana 44

Garbage collector - Krátkodobé objekty
Mnoho objektů v Pythonu existuje jen velmi krátce – často jen po dobu jednoho
výrazu.
Dočasný objekt
1 print ( len ([1,2,3]))
Seznam je vytvořen pouze jako argument
funkce len . Po vyhodnocení výrazu na něj
již nic neodkazuje.
Lokální proměnná
1 def f():
2 x = [1,2,3]
3 return sum (x)
4
5 f()
Objekt existuje jen během běhu funkce. Po
návratu z funkce obvykle zanikne, protože
ztratí poslední referenci.
Tyto krátkodobé objekty tvoří velkou část všech alokací v programu.

## Strana 45

Garbage collector - Objekty s delší životností
Objekt může přežít funkci, ve které byl vytvořen, pokud na něj existuje další reference.
Vrácený objekt
1 def make_list():
2 x = [1,2,3]
3 return x
4
5 a = make_list()
Seznam vznikl uvnitř funkce, ale reference
a ho udržuje naživu.
Globální objekt
1 cache = {}
2
3 def store(k, v):
4 cache[k] = v
Objekty uložené ve slovníku mohou žít po
celou dobu běhu programu.
Životnost objektu tedy neurčuje místo v kódu, ale existence referencí.

## Strana 46

Garbage collector - Objekt udržovaný jiným objektem
Objekt může přežít i po odstranění jména, pokud je uložen v jiné struktuře.
1 items = []
2
3 x = [1,2,3]
4 items.append(x)
5
6 del x
7
8 print (items)
Interpretace:
▶ jméno x zmizí
▶ seznam ale stále existuje
▶ důvodem je reference uložená v items
Příkaz del tedy maže jméno, nikoliv nutně samotný objekt.

## Strana 47

Garbage collector - Referenční cyklus
Objekty mohou vytvářet cykly, které reference counting nedokáže odstranit.
1 a = []
2 b = []
3
4 a.append(b)
5 b.append(a)
Vznikne struktura:
a → b → a
Pokud nyní odstraníme jména
1 del a
2 del b
objekty na sebe stále odkazují. Takové struktury musí později odstranit garbage
collector.

## Strana 48

Závěr

## Strana 49

Závěr - Shrnutí
▶ Programy pracují s pamětí reprezentovanou adresami.
▶ Stack slouží pro volání funkcí a lokální proměnné.
▶ Heap umožňuje dynamickou alokaci.
▶ Ruční správa paměti může vést k chybám jako memory leak nebo segmentation
fault.
▶ Python používá automatickou správu paměti.
▶ Hlavním mechanismem je reference counting doplněný garbage collectorem.

## Strana 50

Závěr - Obligatory meme
