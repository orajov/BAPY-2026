---
source: input/study_materials/08_execution_model.pdf
title: 08_execution_model
pages: 43
parsed_at: 2026-06-03T19:25:43.020Z
source_mtime: 2026-06-03T19:24:04.803Z
---

# 08_execution_model

## Strana 1

Modely výpočtu a řízení běhu programu
Václav Alt

## Strana 2

Motivace

## Strana 3

Motivace - Řízení výpočtu
Spojením Execution model nemyslíme konkrétní algoritmy, ale způsob, jak řídit
výpočet.
▶ jak problém formulujeme (rekurze vs iterace)
▶ kolikrát něco počítáme (memoizace)
▶ kdy se výpočet provede (lazy evaluation)
▶ jak abstrahujeme chování (higher-order funkce)
Stejný problém lze řešit více způsoby, které se liší:
▶ časovou složitostí
▶ paměťovou náročností
▶ čitelností a modularitou

## Strana 4

Motivace - Příklad: schody
Máme schodiště a můžeme dělat kroky délky 1 nebo 2.
Otázka
Kolika způsoby lze vystoupat na n -tý schod?
0
1
2
3
4
start
cíl
modrá: krok o 1
červená: krok o 2

## Strana 5

Motivace - Naivní řešení
1 def count_ways(n):
2 count = 0
3
4 def explore(path_sum):
5 nonlocal count
6 if path_sum == n:
7 count += 1
8 return
9 if path_sum > n:
10 return
11
12 explore(path_sum + 1)
13 explore(path_sum + 2)
14
15 explore(0)
16 return count
▶ Zkusíme všechny možné
kombinace kroků 1 a 2
▶ spočítáme ty, které dojdou
k n -tému schodu
▶ nepočítáme výsledek přímo, místo
toho generujeme všechny
možnosti a filtrujeme –
Brute-force řešení

## Strana 6

Rekurze

## Strana 7

Rekurze - Schody - Lepší řešení
Hledáme tedy funkci ways : N → N
Můžeme řešit postupně:
▶ 1. schod: 1 způsob: ways (1) = 1
▶ 2. schod: 2 způsoby: ways (2) = 2
▶ 3. schod: 3 způsoby: ways (3) = 3

## Strana 8

Rekurze - Schody - Lepší řešení
Hledáme tedy funkci ways : N → N
Můžeme řešit postupně:
▶ 1. schod: 1 způsob: ways (1) = 1
▶ 2. schod: 2 způsoby: ways (2) = 2
▶ 3. schod: 3 způsoby: ways (3) = 3
▶ n. schod: ways ( n ) = ways ( n − 1) + ways ( n − 2)

## Strana 9

Rekurze - Schody - Lepší řešení
Hledáme tedy funkci ways : N → N
Můžeme řešit postupně:
▶ 1. schod: 1 způsob: ways (1) = 1
▶ 2. schod: 2 způsoby: ways (2) = 2
▶ 3. schod: 3 způsoby: ways (3) = 3
▶ n. schod: ways ( n ) = ways ( n − 1) + ways ( n − 2) - stejné jako Fibonacciho čísla

## Strana 10

Rekurze - Schody - Lepší řešení
Hledáme tedy funkci ways : N → N
Můžeme řešit postupně:
▶ 1. schod: 1 způsob: ways (1) = 1
▶ 2. schod: 2 způsoby: ways (2) = 2
▶ 3. schod: 3 způsoby: ways (3) = 3
▶ n. schod: ways ( n ) = ways ( n − 1) + ways ( n − 2) - stejné jako Fibonacciho čísla
▶ Rekurze odpovídá přirozené struktuře problému
▶ Problém se rozpadá na podproblémy stejného typu
▶ Celkové řešení umíme poskládat jako kombinaci dílčích

## Strana 11

Rekurze - Definice
Co je vlastně rekurze?
Rekurze je programovací technika, při níž je určitá procedura nebo funkce
znovu volána dříve, než je dokončeno její předchozí volání.
▶ Výhodou rekurze je, že často dobře odpovídá matematickému popisu problému
▶ Nevýhodou může být vyšší výpočetní náročnost (časová i paměťová)

## Strana 12

Rekurze - Rekurzivní implementace schodů
1 def ways(n):
2 if n <= 1:
3 return 1
4 return ways(n-1) + ways(n-2)
Vlastnosti:
▶ velmi přímočará implementace
▶ odpovídá matematickému zápisu
Problém:
▶ stejná hodnota se počítá opakovaně

## Strana 13

Rekurze - Problém rekurze
ways(5)
ways(4)
ways(3)
ways(2)
ways(1) ways(0)
ways(1)
ways(2)
ways(1) ways(0)
ways(3)
ways(2)
ways(1) ways(0)
ways(1)

## Strana 14

Rekurze - Problém rekurze
Rekurzivní volání vytváří strom výpočtu:
▶ ways ( n ) volá ways ( n − 1) a ways ( n − 2)
▶ ty dále volají své podproblémy
Důsledek:
▶ exponenciální počet volání
▶ dramaticky pomalé pro větší n
Klíčový problém:
▶ opakované výpočty stejných hodnot

## Strana 15

Memoizace

## Strana 16

Memoizace - Myšlenka memoizace
Pokud jsme již spočítali ways ( k ) :
▶ není nutné ho počítat znovu
Použijeme cache:
▶ uložíme si výsledky mezivýpočtů
Změna:
▶ neměníme definici problému
▶ měníme způsob provádění výpočtu
Už jsme viděli v kapitole o dekorátorech

## Strana 17

Memoizace - Dynamické programování
▶ problém lze rozložit na menší podproblémy
▶ stejné podproblémy se opakují
Myšlenka:
▶ výsledek každého podproblému spočítáme jen jednou
▶ a uložíme si ho pro další použití
Dva základní přístupy:
shora dolů: rekurze + memoizace
zdola nahoru: tabelizace / iterace

## Strana 18

Memoizace - Memoizace v Pythonu
1 from functools import lru_cache
2
3 @lru_cache
4 def ways(n):
5 if n <= 1:
6 return 1
7 return ways(n-1) + ways(n-2)
▶ stejné rozhraní funkce
▶ dramatické zrychlení
▶ fakticky aplikace dynamického programování na úlohu se schody

## Strana 19

Iterace

## Strana 20

Iterace - Problém rekurze (znovu)
▶ rekurze používá zásobník volání
▶ nemáme kontrolu nad:
▶ pamětí
▶ pořadím výpočtu
Otázka:
▶ můžeme řídit výpočet explicitně?

## Strana 21

Iterace - Rekurze vs Iterace
Rekurze Iterace
implicitní stack explicitní stav
funkce volá sama sebe smyčka
snadná formulace kontrola průběhu
méně kontrolovatelná efektivní
Interpretace
▶ rekurze = co počítáme
▶ iterace = jak to počítáme

## Strana 22

Iterace - Iterace jako přechod stavů
( a , b ) → ( b , a + b )
▶ stav = aktuální hodnoty
▶ každý krok:
▶ přechod do nového stavu
Důležité
▶ žádný stack
▶ žádná rekurze
▶ plná kontrola nad výpočtem

## Strana 23

Iterace - Iterativní implementace
1 def ways_iter(n):
2 a, b = 1, 1
3 for _ in range (n):
4 a, b = b, a + b
5 return a
Srovnání:
▶ rekurze: implicitní struktura
▶ iterace: explicitní řízení

## Strana 24

Iterace - Memoizace vs Iterace (DP)
▶ memoizace:
▶ top-down
▶ ukládáme výsledky
▶ iterace:
▶ bottom-up
▶ počítáme postupně

## Strana 25

Řízení času výpočtu

## Strana 26

Řízení času výpočtu - Kdy počítáme?
Dosud:
▶ funkce vrací konkrétní hodnotu
Otázka:
▶ Co když chceme více hodnot?
▶ Co když nepotřebujeme všechny najednou?
Řešení: Lazy evaluation
▶ výpočet odložíme až do chvíle, kdy je výsledek třeba.
Klasický příklad:
1 N = 100_000_000
2 # list comprehension spocita vse okamzite (muze trvat)
3 lst = [2*x for x in range (N)]
4 # generator expression pocita hodnoty postupne, az kdyz je potrebujeme
5 gen = (2*x for x in range (N))

## Strana 27

Řízení času výpočtu - Generátor
1 def ways_seq():
2 a, b = 1, 1
3 while True:
4 yield a
5 a, b = b, a + b
6
7 g = ways_seq()
8 [ next (g) for _ in range (6)] # [1, 1, 2, 3, 5, 8]
Použití:
▶ hodnoty se generují postupně
▶ počítají se až při požadavku

## Strana 28

Řízení času výpočtu - yield jako pozastavení výpočtu
Co dělá yield ?
▶ mění funkci na generátor
▶ kromě návratu navíc pozastaví běh funkce
▶ další volání pokračuje od stejného místa
1 def gen():
2 print ("start")
3 yield 1
4 print ("middle")
5 yield 2
1 g = gen()
2 next (g) # start -> 1
3 next (g) # middle -> 2
Klíčová vlastnost
▶ lokální proměnné i pozice v kódu se zachovají

## Strana 29

Higher-order funkce

## Strana 30

Higher-order funkce - Funkce jako objekty
V Pythonu:
▶ first-class citizen – funkce jsou objekty jako všechno ostatní
▶ funkce lze předávat jako argumenty
▶ funkce lze vracet
Higher-order funkce
Funkce, které přijímají funkci jako parametr nebo funkci navracejí.
To umožňuje:
▶ abstrahovat chování
▶ oddělit logiku od řízení

## Strana 31

Higher-order funkce - Closure (uzávěr) – obecná idea
Motivace
▶ funkce používá proměnné ze svého okolí
▶ co když toto okolí zanikne?
Definice
▶ closure = funkce + zachycené prostředí
▶ funkce si “pamatuje” proměnné z místa svého vzniku
Intuice
▶ funkce není jen kód
▶ je to kód + kontext

## Strana 32

Higher-order funkce - Closure v Pythonu
1 def make_adder(a):
2 def adder(x):
3 return x + a
4 return adder
5
6 add5 = make_adder(5)
7 add5(10) # 15
Co se děje?
▶ adder používá proměnnou a
▶ a není lokální ani globální
▶ Python ji uloží do closure
Technicky
▶ funkce má atribut __closure__
▶ obsahuje zachycené proměnné
(cell objects)
1 add5.__closure__
Důsledek
▶ closure umožňuje:
▶ návrat funkcí
▶ dekorátory
▶ zapouzdření stavu bez tříd

## Strana 33

Higher-order funkce - Vlastní cache jako funkce
1 def cache(f):
2 memory = {}
3
4 def inner(n):
5 if n not in memory:
6 memory[n] = f(n)
7 return memory[n]
8
9 return inner

## Strana 34

Higher-order funkce - Použití cache
1 @cache
2 def ways(n):
3 if n <= 1:
4 return 1
5 return ways(n-1) + ways(n-2)
Pozorování:
▶ algoritmus se nemění
▶ mění se způsob provádění
cache v příkladu
▶ je dekorátor - upravuje chování jiné funkce
▶ je HOF, protože
▶ přijímá funkci jako parametr
▶ navrací funkci
▶ využívá closure – navrácená funkce inner má přístup k memory

## Strana 35

Lambda funkce

## Strana 36

Lambda funkce - Definice
Anonymní funkce:
▶ krátký zápis
▶ bez jména
Použití:
▶ lokální transformace
▶ jednoduché operace

## Strana 37

Lambda funkce - Příklad
1 data = [1, 2, 3, 4]
2
3 squared = list ( map ( lambda x: x*x, data))
Alternativa:
▶ klasická funkce pomocí def
Lambda je vhodná pro:
▶ krátké, jednorázové funkce

## Strana 38

Rekurze podruhé

## Strana 39

Rekurze podruhé - Druhy rekurze
Rozlišujeme dva druhy rekurze, tzv. head recursion a tail recursion , podle toho, kde
v těle funkce se nachází rekurzivní volání
1 # napred rekurze, potom prace
2 function head(n):
3 if n == 0:
4 return base_value
5
6 result = head(n - 1)
7 return combine(result, n)
1 # napred prace, rekurze na konci
2 function tail(n, acc):
3 if n == 0:
4 return acc
5
6 return tail(n - 1, update(acc, n))
U tail rekurze se typicky celý stav pře-
dává funkci ( acc )

## Strana 40

Rekurze podruhé - Přechod od rekurze k cyklu
▶ Rekurze je někdy špatně čitelná, pomalá či paměťově náročná
▶ v cyklu máme lepší kontrolu na zdroji a průběhem výpočtu
▶ tail rekurzi lze vždy převést na cyklus:
1 # tail-rekurzivni verze
2 function f(x, y, ...):
3 if condition(x, y):
4 return result(x, y)
5
6 return f(x', y', ...)
1 # verze s cyklem
2 function f(x, y, ...):
3 while not condition(x, y):
4 (x, y, ...) = (x', y', ...)
5
6 return result(x, y)

## Strana 41

Rekurze podruhé - Faktoriál
n ! = n · ( n − 1) · ( n − 2) . . . 2 · 1
1 function fact_head(n):
2 if n == 1:
3 return 1
4 result = fact_head(n - 1)
5 return n * result
1 # napred prace, rekurze na konci
2 function fact_tail(n, acc):
3 if n == 0:
4 return acc
5
6 return fact_tail(n - 1, acc * n)

## Strana 42

Shrnutí

## Strana 43

Shrnutí - Sjednocení
Různé techniky řeší různé aspekty výpočtu:
▶ rekurze: struktura problému
▶ iterace: řízení výpočtu
▶ memoizace: odstranění opakování
▶ lazy evaluation: kdy se počítá
▶ higher-order funkce: abstrakce chování
▶ lambda: lokální definice chování
Všechny lze chápat jako způsoby řízení výpočtu.
