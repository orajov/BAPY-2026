---
source: input/study_materials/05_numpy.pdf
title: 05_numpy
pages: 35
parsed_at: 2026-06-03T19:25:42.975Z
source_mtime: 2026-06-03T19:24:04.808Z
---

# 05_numpy

## Strana 1

Numpy
Václav Alt

## Strana 2

Motivace

## Strana 3

Motivace - Práce s větším množstvím čísel
▶ V Pythonu můžeme pracovat s čísly velmi pohodlně:
▶ Pokud ale chceme provést operaci nad celým polem:
1 a = [1, 2, 3]
2 b = [4, 5, 6]
3 result = []
4 for x, y in zip (a, b):
5 result.append(x + y)
Tento styl práce má dvě zásadní nevýhody:
▶ velké množství explicitních cyklů
▶ každá operace probíhá v Python interpreteru
Pro malé úlohy to nevadí, ale u milionů prvků je Python pomalý.

## Strana 4

Motivace - Srovnání
Python seznamy:
1 a = [1, 2, 3]
2 b = [4, 5, 6]
3 result = []
4 for x, y in zip (a, b):
5 result.append(x + y)
NumPy:
1 a = np.array([1, 2, 3])
2 b = np.array([4, 5, 6])
3 a + b

## Strana 5

Motivace - Numerické výpočty v Pythonu
V numerických úlohách se často objevují operace nad celými poli:
▶ vektory
▶ matice
▶ signály
▶ obrazy
▶ velké datové tabulky
Typické operace:
▶ součet dvou vektorů
▶ výpočet statistiky
▶ lineární algebra
▶ transformace dat

## Strana 6

Motivace - NumPy
NumPy je knihovna, která poskytuje:
▶ efektivní reprezentaci numerických polí
▶ rychlé operace nad celými poli
▶ základní nástroje lineární algebry
▶ generování náhodných čísel
▶ …
Základní myšlenka:
▶ Místo práce s jednotlivými čísly provádíme operace nad celými poli.
▶ Velká část výpočtu probíhá v optimalizovaném C kódu.

## Strana 7

ndarray

## Strana 8

ndarray - Základní objekt ndarray
Základní datová struktura NumPy je:
ndarray (n-dimensional array)
▶ homogenní pole hodnot
▶ pevný datový typ
▶ libovolný počet dimenzí
Příklady:
▶ vektor
▶ matice
▶ 3D pole (např. obraz)

## Strana 9

ndarray - Základní vlastnosti pole
1 a = np.array([1,2,3,4])
Důležité atributy:
1 a.shape
2 a.dtype
3 a.ndim
4 a.size
▶ shape — rozměry pole
▶ dtype — datový typ prvků
▶ ndim — počet dimenzí
▶ size — celkový počet prvků

## Strana 10

ndarray - Vytvoření NumPy pole
▶ Pro základní tvorbu polí poslouží výchozí konstruktor, který přijímá běžné typy na
vstupu:
1 import numpy as np
2
3 a = np.array([1, 2, 3, 4])
▶ K dispozici i řada speciálních konstruktorů
1 np.zeros(5) # pole 5 nul
2 np.ones(3) # pole 3 jednicek
3 np.empty(10) # pole 10 nespecifikovaných hodnot
4 np.full(10, 2.) # pole 10 float 2
Výsledkem je vždy objekt typu numpy.ndarray

## Strana 11

ndarray - Vytvoření NumPy pole II
Velmi užitečné jsou funkce np.linspace(start, stop, count)
a np.arange(start, stop, step)
1 >>> np.linspace(0, 1, 10) # vytvori presne n=10 bodu
2 array([0. , 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1. ])
3 >>> np.arange(0, 1, 0.1) # pouziva krok step=0.1
4 array([0. , 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9])
V praxi kombinujeme tyto konstruktory s argumenty jako shape a dtype (případně
reshape ) k vytváření polí na míru:
1 >>> np.zeros(shape=(2,3), dtype= float )
2 array([[0., 0., 0.],
3 [0., 0., 0.]])
4 >>> np.array([1, 2, 3], dtype=np.complex128).reshape((3,1))
5 array([[1.+0.j],
6 [2.+0.j],
7 [3.+0.j]])

## Strana 12

ndarray - Indexování
Indexování je podobné Python seznamům.
1 a = np.arange(10)
2
3 a[3]
4 a[2:6]
U vícerozměrných polí:
1 m[0,1] # prvni radek
2
3 m[:,1] # druhy sloupec
Jako index používáme:
▶ celé číslo (int)
▶ řezy (slices)
▶ kombinaci obojího

## Strana 13

ndarray - Views vs copies
Mnoho operací v NumPy nevytváří nová data, ale pouze pohled (view) na existující
pole.
▶ slicing obvykle vytváří view
▶ změna view změní i původní pole
▶ kopii lze vytvořit explicitně pomocí copy()
1 a = np.arange(10)
2 b = a[2:5] # view
3 b[0] = 100
4 print (a)
5 # [0 1 100 3 4 5 6 7 8 9]
1 c = a[2:5].copy()

## Strana 14

ndarray - Operace podél os
Mnoho funkcí NumPy provádí operace podél určité osy pole .
▶ axis=0 — operace po sloupcích
▶ axis=1 — operace po řádcích
1 A = np.array([
2 [1,2,3],
3 [4,5,6],
4 [7,8,9]
5 ])
1 np. sum (A) # soucet vsech prvku
2 np. sum (A, axis=0) # soucet sloupcu
3 # [12 15 18]
4 np. sum (A, axis=1) # soucet radku
5 # [6 15 24]

## Strana 15

Co to umí?

## Strana 16

Co to umí? - Elementwise operace
NumPy umožňuje provádět operace nad celými poli. Typicky se jedná o operace po
prvcích (element-wise operation)
Například sečtení
a + b
znamená:
( a 1 + b 1 , a 2 + b 2 , . . . )
Tento styl výpočtu se nazývá vektorizace - operace nad celými poli bez explicitních
cyklů.

## Strana 17

Co to umí? - Další elementwise operace
Většina běžných operací je vektorizována:
1 x = np.arange(5)
2 x * 2
3 x ** 2
4 x + 10
Stejný princip platí pro většinu matematických funkcí.

## Strana 18

Co to umí? - Matematické funkce
NumPy obsahuje velké množství matematických funkcí:
1 np.sin(x)
2 np.exp(x)
3 np.sqrt(x)
Obsahuje také generátory náhodných čísel a základní statistické funkce
1 x = np.random.rand(1000)
2
3 np.mean(x)
4 np.std(x)
5 np. min (x)
6 np. max (x)

## Strana 19

Co to umí? - Lineární algebra
A podporu běžné lineární algebry
1 A = np.random.rand(3,3) # nahodna matice 3x3
2 B = np.random.rand(3,3)
1 A @ B # maticove nasobeni
1 np.linalg.inv(A) # inverzni matice
1 np.linalg.eig(A) # vlastni cisla matice

## Strana 20

Proč je NumPy rychlé

## Strana 21

Proč je NumPy rychlé - Vnitřní struktura NumPy pole
NumPy pole ( ndarray ) je navrženo jako kompaktní blok paměti.
Každé pole se skládá ze dvou částí:
▶ metadata (malý Python objekt)
▶ datový blok (souvislá oblast paměti)
Metadata obsahují například:
▶ shape — rozměry pole
▶ dtype — typ uložených hodnot
▶ strides — krok v paměti mezi prvky jednotlivých dimenzí
▶ ukazatel na začátek dat v paměti
Samotná data jsou uložena jako:
souvislé pole hodnot stejného typu
Například pole typu float64 je ve skutečnosti sekvence 8-bytových čísel uložených
za sebou.
Homogenita

## Strana 22

Proč je NumPy rychlé - Proč je tato struktura rychlá
U Python seznamu jsou prvky uloženy jako ukazatele na objekty.
Python list:
pointer → PyObject
pointer → PyObject
pointer → PyObject
Každý prvek je samostatný Python objekt.
NumPy pole:
[1.0][2.0][3.0][4.0][5.0]
Hodnoty jsou uložené přímo v paměti.
Výhody tohoto uspořádání:
▶ žádná režie Python objektů
▶ efektivní využití CPU cache (+ SIMD instrukce procesoru)
▶ snadná implementace vektorových instrukcía
▶ výpočty mohou běžet v optimalizovaném C kódu

## Strana 23

Proč je NumPy rychlé - Proč jsou Python cykly pomalé
Python musí při každé iteraci provést mnoho kroků:
▶ načíst Python objekt
▶ zkontrolovat typ
▶ zavolat operátor +
▶ vytvořit nový Python objekt
▶ uložit výsledek
Tyto operace probíhají pro každý prvek zvlášť.
NumPy naopak provádí výpočet přibližně takto:
1 for i in range (n):
2 result[i] = a[i] + b[i]
ale tento cyklus je napsaný v C a pracuje přímo s primitivními čísly.

## Strana 24

Proč je NumPy rychlé - Výhody vektorizace
Vektorizace přináší několik důležitých výhod.
1. Výkon
▶ méně práce pro Python interpretér
▶ operace probíhají v optimalizovaném kódu
2. Jednodušší kód
1 y = x**2 + 3*x + 1
místo složitého cyklu.

## Strana 25

Proč je NumPy rychlé - Praktický příklad
Chceme spočítat hodnoty funkce
f ( x ) = sin ( x ) + x
2
pro velké množství bodů.
Python přístup
1 result = []
2 for x in data:
3 result.append(math.sin(x) + x*x)
NumPy přístup
1 x = np.linspace(0,10,1000000)
2
3 y = np.sin(x) + x**2
Celý výpočet proběhne v jediné vektorizované operaci.

## Strana 26

Broadcasting

## Strana 27

Broadcasting - Broadcasting
Broadcasting je mechanismus, který umožňuje provádět operace mezi poli různých
rozměrů bez explicitního rozšiřování dat.
Jednoduchý příklad:
1 x = np.array([1,2,3,4])
1 x + 10
NumPy interpretuje tuto operaci jako:
1 [1,2,3,4] + [10,10,10,10]
Číslo 10 se tedy implicitně „rozšíří“ na pole stejného rozměru jako x .

## Strana 28

Broadcasting - Pravidla
Broadcasting porovnává rozměry polí zprava. Dva rozměry jsou kompatibilní, pokud
1. jsou jejich rozměry (shape) stejné
2. nebo jeden rozměr je 1
Příklady kompatibilních rozměrů:
1 (n, ) + (n, ) -> (n, )
2 (3, 1) + (1, 4) -> (3, 4)
3 (5, 3, 1) + (1, 4) -> (5, 3, 4)

## Strana 29

Broadcasting - Broadcasting u vícerozměrných polí
Broadcasting funguje i u vícerozměrných polí.
Příklad:
1 x = np.array([1,2,3])
2 M = np.ones((3,3))
3 M + x
NumPy interpretuje operaci jako:


1 1 1
1 1 1
1 1 1

 +
[
1 2 3
]
NumPy zarovnává rozměry doprava: vektor x interpretován jako (1,3) a následně
roztažen na (3,3)
Broadcasting umožňuje zapisovat operace nad vektory a maticemi velmi stručně, bez
explicitních cyklů nebo kopírování dat.

## Strana 30

Broadcasting - Broadcasting vs operace podél os
Dva často zaměňované mechanismy NumPy:
Broadcasting
Rozšiřuje pole tak, aby bylo možné provést elementwise operaci .
Vektor x je interpretován jako (1,3) a roztažen na (3,3) .
Operace podél os
Redukuje pole – snižuje počet dimenzí .
1 np. sum (M, axis=0) # soucet sloupcu
2 np. sum (M, axis=1) # soucet radku

## Strana 31

Ekosystém

## Strana 32

Ekosystém - Ekosystém vědeckého Pythonu
NumPy je základní stavební kámen vědeckého Pythonu.
▶ NumPy — numerická pole
▶ SciPy — pokročilé numerické metody
▶ Pandas — práce s tabulkovými daty
▶ Matplotlib — grafy
▶ scikit-learn — strojové učení
Velká část těchto knihoven používá NumPy pole jako základní datovou strukturu.

## Strana 33

Ekosystém - Typické použití NumPy
NumPy se používá například v oblastech:
▶ vědecké výpočty
▶ zpracování dat
▶ simulace
▶ strojové učení
▶ zpracování obrazu
Mnoho knihoven očekává NumPy pole jako vstup.

## Strana 34

Závěr

## Strana 35

Závěr - Shrnutí
NumPy poskytuje:
▶ datovou strukturu ndarray
▶ efektivní reprezentaci numerických dat
▶ vektorové operace nad poli
▶ základní nástroje numerických výpočtů
Hlavní princip:
Místo explicitních cyklů používáme operace nad celými poli.
