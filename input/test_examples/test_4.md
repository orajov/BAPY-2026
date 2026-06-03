---
source: input/test_examples/test_4.pdf
title: test_4
pages: 2
parsed_at: 2026-06-03T19:44:52.160Z
source_mtime: 2026-06-03T19:27:20.351Z
---

# test_4

## Strana 1

test_4.md 2026-03-17
1 / 2
Test 4 – Iterátory a Context Managery
Jméno a přijímení: ________________________________________
1. Uvažujte následující fragment kódu:
```python
numbers = [1, 2, 3]
it = iter(numbers)
print(next(it))
print(next(it))
```
Otázka A: Které z následujících tvrzení je pravdivé?
A) numbers je iterátor a it je iterovatelný objekt.
B) numbers je iterovatelný objekt a it je iterátor.
C) Oba objekty jsou iterátory, protože oba lze použít ve for cyklu.
D) Mezi numbers a it není žádný rozdíl, iter() pouze vytvoří kopii seznamu.
Otázka B: Co se stane, pokud zavoláme next(it) ještě třikrát?
A) Program se vrátí na začátek a vypíše opět 1.
B) Program vypíše None .
C) Vyvolá se výjimka StopIteration .
D) Vyvolá se výjimka IndexError .
2. Mějme vlastní třídu, kterou chceme použít v cyklu for :
```python
class MyRange:
    def __init__(self, stop):
        self.current = 0
        self.stop = stop
    def __iter__(self):
    return self
    def __next__(self):
        if self.current < self.stop:
val = self.current
self.current += 1
return val
raise StopIteration
```

## Strana 2

test_4.md 2026-03-17
2 / 2
Jaká metoda je nezbytná k tomu, aby objekt mohl být označen jako "Iterovatelný" (Iterable) a mohl tak
vůbec vstoupit do for cyklu?
A) Pouze metoda __next__ .
B) Pouze metoda __getitem__ .
C) Metoda __iter__ , která vrací objekt s metodou __next__ .
D) Metoda __run__ .
3. Uvažujte třídu, která spravuje připojení k databázi:
```python
class DatabaseConnection:
    def __enter__(self):
        print("Connecting...")
    return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Closing connection...")
```
# Použití:
with DatabaseConnection() as db:
```python
print("Working with DB")
```
Kdy přesně se vykoná kód uvnitř metody __exit__ ?
A) Pouze v případě, že v bloku with dojde k chybě.
B) Ihned po zavolání DatabaseConnection(), ještě před začátkem bloku with.
C) Vždy po skončení bloku with (ať už proběhl v pořádku, nebo s chybou).
D) Metoda __exit__ se v tomto kódu nevykoná, musí se volat ručně jako db.exit() .
