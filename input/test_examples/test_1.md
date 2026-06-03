---
source: input/test_examples/test_1.pdf
title: test_1
pages: 2
parsed_at: 2026-06-03T19:44:52.115Z
source_mtime: 2026-06-03T19:27:20.313Z
---

# test_1

## Strana 1

test_1.md 2026-02-23
1 / 2
Test 1 – Dědičnost, abstraktní třída a metoda
Jméno a přijímení: ________________________________________
1. V kontextu OOP v Pythonu dědičnost znamená, že:
A) Instance (objekt) získá všechny atributy jiné instance stejné třídy při jejím kopírování.
B) Nově definovaná třída (potomek) přebírá atributy a metody z již existující třídy (rodiče).
C) Funkce přijímá jinou funkci jako argument a rozšiřuje její původní funkcionalitu.
D) Třída je definována jako abstraktní a nelze z ní vytvořit žádnou instanci.
2. Které z následujících tvrzení o abstraktních třídách v Pythonu je pravdivé?
A) Abstraktní třídy jsou v Pythonu definovány automaticky, pokud třída nemá žádné metody.
B) Pro vytvoření abstraktní třídy je nutné dědit z třídy ABC z modulu abc.
C) Z abstraktní třídy lze vytvořit instanci (objekt) úplně stejně jako z běžné třídy.
D) Abstraktní třída nesmí obsahovat žádné konkrétní (implementované) metody.
3. Co se stane, pokud ve třídě, která dědí z abstraktní třídy, nepřepíšete (neimplementujete)
metodu označenou dekorátorem @abstractmethod ?
A) Program se normálně spustí, ale při zavolání dané metody vyhodí chybu NotImplementedError.
B) Python automaticky doplní prázdnou implementaci (pass).
C) Při pokusu o vytvoření instance této podtřídy dojde k chybě (TypeError).
D) Abstraktní metody se v Pythonu nemusí implementovat, jsou pouze dokumentační.
4. K čemu slouží funkce super() v metodě __init__ potomka?
A) K přepsání (override) metod rodičovské třídy tak, aby přestaly fungovat.
B) K zavolání konstruktoru (nebo jiné metody) rodičovské třídy, aby se správně inicializovaly zděděné
atributy.
C) K vytvoření nové instance abstraktní třídy uvnitř potomka.
D) K ukončení dědičnosti a převedení třídy na statickou.
5. Při spuštění následujícího programu dojde k chybě (TypeError). Prozkoumejte kód a určete, co je
její příčinou:

## Strana 2

test_1.md 2026-02-23
2 / 2
```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, name: str) -> None:
        self.name = name
    @abstractmethod
    def start_engine(self) -> None:
        pass

class Car(Vehicle):
    def start_engine(self) -> None:
        print(f"{self.name}: Vrmmm, motor auta běží!")
        # --- Spuštění ---
my_car = Car("Audi")
my_vehicle = Vehicle("Bike")
```
