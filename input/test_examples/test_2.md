---
source: input/test_examples/test_2.pdf
title: test_2
pages: 2
parsed_at: 2026-06-03T19:44:52.145Z
source_mtime: 2026-06-03T19:27:20.356Z
---

# test_2

## Strana 1

test_2.md 2026-03-02
1 / 2
Test 1 – Vícenásobná dědičnost
Jméno a přijímení: ________________________________________
1. V Pythonu znamená vícenásobná dědičnost, že:
A) Třída může dědit atributy a metody pouze z jedné rodičovské třídy.
B) Třída může dědit atributy a metody z více než jedné rodičovské třídy.
C) Třída musí mít všechny metody z rodičů implementované, jinak se program nespustí.
D) Vícenásobná dědičnost není v Pythonu podporována.
2. Uvažujte následující dědičnost:
```python
class A:
    def greet(self):
        print("Hello from A")

class B(A):
    def greet(self):
        print("Hello from B")

class C(A):
    def greet(self):
        print("Hello from C")

class D(B, C):
    pass
d = D()
d.greet()
```
Otázka: Co se vypíše při zavolání d.greet() a proč?
A) Hello from A – protože metoda se dědí z nejvyšší třídy.
B) Hello from B – protože Python používá MRO (Method Resolution Order).
C) Hello from C – protože C je napsaná později ve výčtu rodičů.
D) Chyba – kvůli diamond problem.
3. K čemu se v Pythonu používají mixiny?
A) K vytvoření samostatné třídy, ze které nelze dědit.
B) K přidání konkrétní funkčnosti do třídy pomocí dědičnosti, aniž by mixin představoval hlavní typ
objektu.

## Strana 2

test_2.md 2026-03-02
2 / 2
C) K nahrazení abstraktních tříd.
D) K automatickému generování metod __init__ .
4. Je dán následující kód:
```python
class LoggerMixin:
    def log(self, message):
        print(f"[LOG]: {message}")

class Worker:
    def work(self):
        print("Working...")

class LoggingWorker(LoggerMixin, Worker):
    pass
lw = LoggingWorker()
lw.work()
lw.log("Done!")
```
Otázka: Co vypíše program a proč je mixin vhodný v tomto případě?
A) Working... a [LOG]: Done! – mixin přidává jen extra funkčnost.
B) Working... – logovací metoda se nepřenese.
C) [LOG]: Done! – metoda work se nepřenese.
D) Chyba – mixiny nelze kombinovat s běžnými třídami.
