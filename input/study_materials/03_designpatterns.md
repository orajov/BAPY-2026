---
source: input/study_materials/03_designpatterns.pdf
title: 03_designpatterns
pages: 54
parsed_at: 2026-06-03T19:25:42.859Z
source_mtime: 2026-06-03T19:24:04.793Z
---

# 03_designpatterns

## Strana 1

Design patterns
Václav Alt

## Strana 2

UML

## Strana 3

UML - Co to
Wiki
The Unified Modeling Language (UML) is a general-purpose, developmental
modeling language in the field of software engineering that is intended to
provide a standard way to visualize the design of a system.

## Strana 4

UML - Přehled vztahů
UML popisuje následující vztahy mezi objekty v programu
▶ Dědičnost
▶ Implementace rozhraní
▶ Asociace
▶ Agregace
▶ Kompozice

## Strana 5

UML - Objekt
MyClass
+ something: str
- _secret: str
+ method(): float
- _another(): float
1 class MyClass:
2 def __init__( self , smth, sec):
3 something = smth
4 _secret = sec
5
6 def method( self ) -> float :
7 ...
8
9 def _another( self ) -> float :
10 ...

## Strana 6

UML - Dědičnost
<< abstract >>
Shape
area(): float
Rectangle
a : float
b : float
area(): float
1 from abc import ABC, abstractmethod
2
3 class Shape(ABC):
4 @abstractmethod
5 def area( self ) -> float : pass
6
7 class Rectangle(Shape):
8 def __init__( self , a, b):
9 self .a = a
10 self .b = b
11
12 def area( self ) -> float :
13 return self .a * self .b

## Strana 7

UML - Interface
<< interface >>
Animal
animalSound()
Pig
animalSound()
1 interface Animal {
2 public void animalSound();
3 }
4
5 class Pig implements Animal {
6 public void animalSound() {
7 System.out.println("The pig says:
oink oink");
8 }
9 }

## Strana 8

<< interface >>
Animal
animalSound()
Pig
animalSound()
1 from typing import Protocol
2
3 class Animal(Protocol):
4 def animalSound( self ) -> None :
5 ...
6
7 class Pig:
8 def animalSound( self ):
9 print ("The pig says: oink
oink")

## Strana 9

UML - Asociace
Logger
log(msg)
DataService
process(data,
logger)
1 class Logger:
2 def log( self , message: str ) ->
None :
3 print (f"[LOG] {message}")
4
5 class DataService:
6 def process( self , data: list [ int ],
logger: Logger) -> int :
7 logger.log("Starting
processing")
8 result = sum (data)
9 logger.log(f"Finished
processing: {result}")
10 return result

## Strana 10

UML - Agregace
Developer
name
Project
name
devs: list[Developer]
▶ Project má více
instancí/referencí na Developer
▶ Developer nezaniká při zániku
Project
1 class Developer:
2 def __init__( self , name: str ):
3 self .name = name
4
5 class Project:
6 def __init__( self , name: str ,
devs: list [Developer]):
7 self .name = name
8 self .devs = devs
▶ weak has-a relation

## Strana 11

UML - Kompozice
OrderItem
name
Order
items
add_item(it,
qty)
▶ Order má více instancí/referencí
na OrderItem
▶ OrderItem zaniká při zániku
Order
1 class OrderItem:
2 def __init__( self , product: str ,
quantity: int ):
3 self .product = product
4 self .quantity = quantity
5
6 class Order:
7 def __init__( self ):
8 self .items: list [OrderItem] =
[]
9
10 def add_item( self , product: str ,
quantity: int ):
11
self .items.append(OrderItem(product,
quantity))
▶ strong has-a relation

## Strana 12

Design Patterns

## Strana 13

Design Patterns - Co to je?
Wiki:
Návrhový vzor (anglicky design pattern) v softwarovém inženýrství představuje
obecné řešení problému, které se využívá při návrhu počítačových programů.
Návrhový vzor není knihovnou nebo částí zdrojového kódu, která by se dala
přímo vložit do našeho programu, jedná se o popis řešení problému nebo šab-
lonu, která může být použita v různých situacích…

## Strana 14

▶ ustálená řešení ustálených problémů
▶ standardizace a slovník
▶ jistá forma abstrakce
▶ ”improve quality of code” - sporné

## Strana 15

Design Patterns - Původ pojmu
▶ Gamma, Erich and Helm, Richard
and Johnson, Ralph and Vlissides,
John, Design Patterns: Elements
of Reusable Object-Oriented
Software , Addison-Wesley, 1994,
ISBN 978-0201633610.
▶ ”Gang of Four” - GoF
▶ napsáno pro C++
▶ 23 návrhových vzorů
▶ považováno za standard

## Strana 16

Design Patterns - 23 DP
Structural
▶ Adapter
▶ Bridge
▶ Composite
▶ Decorator
▶ Facade
▶ Flyweight
▶ Proxy
Creational
▶ Abstract Factory
▶ Builder
▶ Factory
▶ Prototype
▶ Singleton
Behavioral
▶ Chain of responsibility
▶ Command
▶ Interpreter
▶ Iterator
▶ Mediator
▶ Memento
▶ Observer
▶ State
▶ Strategy
▶ Template method
▶ Visitor

## Strana 17

Design Patterns - Literatura a zdroje
▶ refactoring.guru
▶ Game programming patterns, Robert Nystrom
▶ Gang of Four - Design Patterns
▶ kanál Arjan codes - Python, hezké příklady použití

## Strana 18

Design Patterns - Jak návrhový vzor popisujeme:
▶ Name and classification
▶ Intent
▶ Also known as
▶ Motivation
▶ Applicability
▶ Structure
▶ Participants
▶ Collaboration
▶ Consequences
▶ Implementation
▶ Sample code

## Strana 19

Design Patterns - Vliv jazyka
Python
▶ interpretovaný
▶ dynamicky typovaný
▶ neumí přetěžování funkcí
▶ méně restrikcí (typy často konvence,
type hints)
▶ stručnější
C++
▶ kompilovaný
▶ staticky typovaný
▶ umí přetěžování funkcí
▶ typy součástí rozhraní, silná
compile-time kontrola
▶ ukecanější

## Strana 20

Design Patterns - OOP
▶ DP často předpokládají podporu O bjektově O rientovaného P rogramování
▶ Idea : sdružit data a relevantní operace do nějakých logických, pojmenovaných
celků.
▶ odvozovat z jednoduchých objektů složitější
▶ Klíčová slova:
▶ encapsulation (zapouzdření) - někdy spojeno s omezením přístupu
▶ dědičnost

## Strana 21

Design Patterns - DP v ne-OOP jazyce?
Je možné používat Design Patterns v jazyce, který nepodporuje OOP?
▶ Obecně lze, ale vyžaduje trochu volnější interpretaci DP.
▶ Řada DP aktivně využívá dědičnost a polymorfismus.
▶ Implementovat polymorfismus v ne-OOP jazyce je obtížné
▶ DP je dobré chápat idiomaticky: popisují role a vzájemné role aktérů v programu
Alternativně lze tvrdit:
OOP je DP v ne-OOP jazycích
▶ GoF DP implementované v C:
▶ github.com/huawenyu/Design-Patterns-in-C
▶ https://github.com/jmarkowski/design-patterns

## Strana 22

Adaptér

## Strana 23

Adaptér - Problém
▶ Máme klienta , který očekává určité rozhraní ( Client / Target ).
▶ Máme existující třídu / knihovnu ( Adaptee ), která má jiné rozhraní (jiné názvy
metod, jiné datové struktury, jiný protokol).
▶ Nechceme / nemůžeme měnit ani klienta ani původní implementaci (legacy kód,
externí knihovna, jiné oddělení, zpětná kompatibilita).
▶ Řešení: vložíme Adapter , který převádí volání i data mezi světy.
▶ Typické použití: integrace legacy API, sjednocení různých providerů, migrace mezi
verzemi API.

## Strana 24

Adaptér - Struktura
Client
<< interface >>
Client interface
method(data)
Adapter
- adaptee: Service
method(data)
Service
serviceMethod(data)

## Strana 25

Adaptér - Příklad
Legacy code
▶ Starý python wrapper okolo
výpočetní knihovny
▶ nemůžeme změnit
1 class LegacySimulation:
2 def get_results( self ):
3 # (time, energy)
4 return [
5 (0.0, -1.2),
6 (0.1, -1.18),
7 (0.2, -1.15),
8 ]
Report module
▶ data team napsal nový report
module
▶ nečetli dokumentaci a očekávají
jiné chování
1 class Report:
2 def __init__( self , source):
3 self .source = source
4
5 def generate( self ):
6 data = self .source.fetch()
7 for row in data:
8 print (f"{row['time']}:
{row['energy']}")

## Strana 26

Adaptér - Příklad
Report
source: SimInterface
<< interface >>
SimInterface
fetch()
LegacySimulation
get_results()

## Strana 27

Adaptér - Příklad
Report
source: SimInterface
<< interface >>
SimInterface
fetch()
Adapter
adaptee: LegacySimulation
fetch()
LegacySimulation
get_results()
raw =
self.source.get_results()
return [
"time": t, "energy": e
for t, e in raw
]

## Strana 28

Adaptér - Příklad
1 class LegacySimulation:
2 def get_results( self ):
3 # (time, energy)
4 return [
5 (0.0, -1.2),
6 (0.1, -1.18),
7 (0.2, -1.15),
8 ]
9
10 class Report:
11 def __init__( self , source):
12 self .source = source
13
14 def generate( self ):
15 data = self .source.fetch()
16 for row in data:
17 print (f"{row['time']}:
{row['energy']}")
1 class SimulationAdapter:
2 def __init__( self , simulation:
LegacySimulation):
3 self .simulation = simulation
4
5 def fetch( self ):
6 raw =
self .simulation.get_results()
7 return [
8 {"time": t, "energy": e}
9 for t, e in raw
10 ]

## Strana 29

Strategy pattern

## Strana 30

Strategy pattern - ukázka kompozice
1 class Logger:
2 def __init__( self , log_strategies):
3 self .log_strategies =
log_strategies
4
5 def write_message( self , message):
6 for strategy in
self .log_strategies:
7 strategy.log(message)
8
9 class LogStrategy:
10 def log( self , message):
11 pass
12
13 class ConsoleLogStrategy(LogStrategy):
14 def log( self , message):
15 print (f"Console: {message}")
16 class FileLogStrategy(LogStrategy):
17 def __init__( self , file_path):
18 self .file_path = file_path
19
20 def log( self , message):
21 with open ( self .file_path, "a")
as log_file:
22 log_file.write(f"File:
{message}\n")
23
24 logger = Logger([ConsoleLogStrategy(),
FileLogStrategy("log.txt")])

## Strana 31

Strategy pattern - ukázka kompozice
Logger
strategies
write_message(message)
<< interface >>
LogStrategy
log(message)
FileLogStrategy
log(message)
ConsoleLogStrategy
log(message)

## Strana 32

Strategy pattern - ukázka kompozice
Context
strategy
do_something()
<< interface >>
Strategy
execute(data)
ConcreteStrategies
execute(data)
ConcreteStrategies
execute(data)

## Strana 33

Dekorátor

## Strana 34

Dekorátor - co to je
▶ Návrhový vzor
▶ Dekorátor umožňuje opakovatelným způsobem rozšiřovat funkcionalitu existujícího
kódu tak, že jej obalí dalším kódem
▶ někdy označován jako wrapper
▶ V Pythonu mají dekorátory zvláštní postavení

## Strana 35

Dekorátor - Ilustrace

## Strana 36

Dekorátor - UML

## Strana 37

Dekorátor - Zjednodušený příklad
1 def add(x, y):
2 return x + y
▶ přidejme něco navíc: oznámení, že byla funkce volána
▶ nesahejme na její definici
▶ napíšeme wrapper - novou funkci, která tu původní obalí
4 def wrapper(x, y):
5 print ("calling function add")
6 return add(x, y)
7
8 wrapper(1, 2)
9 # ---
10 # calling function add
11 # 3

## Strana 38

Dekorátor - Obecnější příklad
▶ napišme funkci, která vrátí wrapper k předané funkci
▶ můžeme tak obalit libovolnou funkci dvou argumentů
1 def better_wrapper(func):
2 def wrapper(x, y):
3 print (f"calling function {func.__name__}")
4 return func(x, y)
5 return wrapper
6
7 def multiply(x, y):
8 return x * y
9
10 wrapped_multiply = better_wrapper(multiply)
11 wrapped_multiply(1, 2)
12 # ---
13 # calling function multiply
14 # 2

## Strana 39

Dekorátor - Zcela obecně
▶ dovolme libovolné množství argumentů
▶ pojmenujme naši wrapper factory log_calls
▶ taková konstrukce už umí obalit úplně libovolnou funkci
1 def log_calls(func):
2 def wrapper(*args, **kwargs):
3 print (f"calling function {func.__name__}")
4 return func(*args, **kwargs)
5 return wrapper
6
7 def some_function(arg1, **kwargs):
8 print (arg1, kwargs.keys())
9
10 logged_some_function = log_calls(some_function)
11 logged_some_function( True , x=3)
12 # ---
13 # calling function some_function
14 # True dict_keys(['x'])

## Strana 40

Dekorátor - celou dobu to byl dekorátor
▶ funkce, která vrácí obalenou funkci, je vlastně dekorátorem
▶ rozšiřuje funkcionalitu existujícího objektu
▶ v Pythonu je možné dekorovat funkce již při definici – nemusíme zavádět nová
jména pro dekorované varianty
▶ k decoraci slouží syntactic sugar @decorator_name
1 @log_calls
2 def another_function():
3 print ("this function does not actually do anything")
4
5 another_function()
6 # ---
7 # calling function another_function
8 # this function does not actually do anything

## Strana 41

Dekorátor - Příklad
▶ chování dekorátoru lze i parametrizovat
▶ wrapper – obaluje funkci
▶ dekorátor – předanou funkci obaluje wrapperem: decorator: func -> wrapper
▶ parametrizovaný dekorátor – vrací dekorátor. Je to tedy funkce, která vrací funkci,
která vrací funkci
1 def log(do_log):
2 def dec(func):
3 def wrapper(*args, **kwargs):
4 if do_log:
5 print (f"calling function
{func.__name__}")
6 return func(*args, **kwargs)
7 return wrapper
8 return dec
10 @log( True )
11 def add(x, y):
12 return x + y
13
14 @log( False )
15 def multiply(x, y):
16 return x * y
17
18 add(1, 2)
19 multiply(1, 2)
20 # ---
21 # calling function add
22 # 3

## Strana 42

Dekorátor - Příklad
▶ funkce log vyrábí různé dekorátory v závislosti na tom, jaký argument jí předáme.
▶ do_log==True vrací dekorátor, který k dekorované funkci přidá print .
▶ do_log==False vrací triviální dekorátor, který nic nedělá.
▶ můžeme přepínat globálně
1 enable_logging = True
2
3
4 @log(enable_logging)
5 def add(x, y):
6 return x + y
7
8 @log(enable_logging)
9 def multiply(x, y):
10 return x * y
11
12 add(1, 2)
13 multiply(1, 2)

## Strana 43

Použití

## Strana 44

Použití - Měření času
▶ Dekorátor je poměrně milý způsob, jak snadno k funkci přidat měření času.
▶ Použijme k tomu balík time , pomocí kterého si pouze zaznamenáme čas před
a po spuštění měřené funkce.
1 import time
2
3 def timer(func):
4 def wrapper(*args, **kwargs):
5 start = time.time()
6 result = func(*args, **kwargs)
7 end = time.time()
8 elapsed_time = end - start
9 print (f"Elapsed time: {elapsed_time} seconds")
10 return result
11 return wrapper

## Strana 45

Použití - Memoizace
▶ Naivní implementace výpočtu Fibonacciho čísel obvykle velmi rychle zaběhne do
hluboké a široké rekurze, což je velmi pomalé.
▶ Demonstrujme si to s použitím měřiče z předchozího příkladu.
1 def fibonacci(n):
2 if n <= 0:
3 return 0
4 elif n == 1:
5 return 1
6 else :
7 return fibonacci(n-1) + fibonacci(n-2)
8
9 timed_fibonacci = timer(fibonacci)
10
11 timed_fibonacci(38) # tohle trvá dlouho

## Strana 46

Použití - Memoizace
▶ k výpočtu n-tého Fibonacciho čísla potřebujeme jen dvě předchozí
▶ výpočet tak lze významně zrychlit přepsáním pomocí for cyklu
a ”zapamatováním” dvou předchozích čísel
▶ takové technice se říká memoizace – jde o uložení výsledků předchozích běhů
a jejich opětovné použití
▶ populární a snadná technika optimalizace řešení náročných úloh (dynamické
programování, průchod herních stromů)
1 @timer
2 def fibonacci_loop(n):
3 a = 0
4 b = 1
5 for _ in range (1, n):
6 a, b = b, a+b
7 return b
8
9 fibonacci_loop(38) # rychlejsi

## Strana 47

Použití - Memoizace
▶ V případě Fibonacciho čísel velmi jednoduché
▶ zkusme obecnější variantu memoizace pomocí dekorátoru
▶ zjednodušme předpokladem, že dekorovaná funkce bude přijímat jediný argument
1 def memoize(func):
2 cache = {}
3 def wrapper(n):
4 if n in cache:
5 return cache[n]
6 result = func(n)
7 cache[n] = result
8 return result
9 return wrapper
11 @memoize
12 def fibonacci(n):
13 if n <= 0:
14 return 0
15 elif n == 1:
16 return 1
17 else :
18 return fibonacci(n-1) +
fibonacci(n-2)
19
20 timed_cached_fibonacci =
timer(fibonacci)
21 timed_cached_fibonacci(38) # hodne
rychle

## Strana 48

Dekorátor v Pythonu

## Strana 49

Dekorátor v Pythonu - Speciální syntaxe
▶ V Pythonu má dekorátor výsadní postavení
▶ svědčí o tom už speciální syntaxe pro dekorování ( @ )
▶ s řadou dekorátorů v Pythonu jsme se již setkali
▶ označení speciálních metod třídy: @classmethod , @staticmethod
▶ označení abstraktní metody třídy: @abstractmethod
▶ definice dataclass pomocí @dataclass

## Strana 50

Dekorátor v Pythonu - Další dekorátory
Python nabízí řadu dalších dekorátorů připravených k použití. Jmenujme dva:
▶ functools.lru_cache – least recently used cache, tj. lépe napsaná
implementace memoizace
▶ contextlib.contextmanager – vyrobí context manager (pro použití s with )
z generátorů (použití klíčového slova yield - o tom jindy)
1 from functools import lru_cache
2
3 @lru_cache
4 def fibonacci(n):
5 if n <= 0:
6 return 0
7 elif n == 1:
8 return 1
9 else :
10 return fibonacci(n-1) + fibonacci(n-2)
11
12 timed_cached_fibonacci = timer(fibonacci)
13 timed_cached_fibonacci(38) # hodne rychle

## Strana 51

Observer

## Strana 52

Observer - Observer: problém
▶ Jeden objekt ( Subject/Publisher ) mění stav nebo generuje události.
▶ Na tyto změny chce reagovat více nezávislých částí systému (logování, UI,
ukládání, metriky, alerty, …).
▶ Nechceme, aby Subject znal všechny závislosti napevno (jinak vzniká těsné
provázání a změny bolí).
▶ Řešení: Observers se přihlásí k odběru a Subject je při události notifikuje.
▶ Výhody: volnější vazba, snadné přidávání/odebírání reakcí za běhu.
▶ Nevýhody: pořadí notifikací a debugování toku událostí může být méně přehledné.

## Strana 53

Observer - Struktura

## Strana 54

Observer - Příklad
1 class Observer:
2 def update( self , event):
3 ...
4
5 class Simulation:
6 def __init__( self ):
7 self ._observers = []
8
9 def subscribe( self , observer):
10
self ._observers.append(observer)
11
12 def _notify( self , event):
13 for obs in self ._observers:
14 obs.update(event)
15
16 def run( self ):
17 for step in range (3):
18 # do computation ...
19 self ._notify({"step":
step})
21 class ConsoleLogger:
22 def update( self , event):
23 print (f"Step {event['step']}
completed")
24
25 class StepCounter:
26 def __init__( self ):
27 self .count = 0
28
29 def update( self , event):
30 self .count += 1
31
32 sim = Simulation()
33
34 sim.subscribe(ConsoleLogger())
35 counter = StepCounter()
36 sim.subscribe(counter)
37
38 sim.run()
