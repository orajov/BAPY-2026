---
source: input/test_examples/test_5.pdf
title: test_5
pages: 2
parsed_at: 2026-06-03T19:44:52.166Z
source_mtime: 2026-06-03T19:27:20.349Z
---

# test_5

## Strana 1

test_5.md 2026-03-23
1 / 2
Test 5 – Návrhové vzory v Pythonu
Jméno a přijímení: ________________________________________
1. Které z následujících tvrzení nejlépe popisuje, co je to "Návrhový vzor" (Design Pattern)?
A) Hotová knihovna, kterou si naimportujeme pomocí import patterns.
B) Opakovatelné a osvědčené řešení běžných problémů při návrhu softwaru.
C) Přesný algoritmus pro řazení dat v paměti.
D) Speciální syntaxe Pythonu, která zrychluje běh programu.
2. Prozkoumejte následující kód. Jaká zpráva se vypíše po zavolání posledního řádku?
```python
from abc import ABC, abstractmethod

class PaymentStrategy(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

class CreditCardPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"Platba kartou: {amount} Kč")

class PayPalPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"Platba přes PayPal: {amount} Kč")

class ShoppingCart:
    def __init__(self, strategy: PaymentStrategy):
        self.strategy = strategy
    def checkout(self, amount):
        self.strategy.pay(amount)
cart = ShoppingCart(PayPalPayment())
cart.checkout(500)
```
A) Platba kartou: 500 Kč
B) Platba přes PayPal: 500 Kč
C) Dojde k chybě, protože ShoppingCart neví, jak platit.
D) Program vypíše obě možnosti platby.
3. Uvažujte následující dekorátor. Co vypíše program po zavolání say_hello()?

## Strana 2

test_5.md 2026-03-23
2 / 2
```python
def uppercase_decorator(func):
    def wrapper():
        result = func()
        return result.upper()
    return wrapper
@uppercase_decorator
def say_hello():
    return "ahoj"
print(say_hello())
```
A) ahoj
B) AHOJ
C) uppercase_decorator
D) Program skončí chybou, protože funkce say_hello nemá argumenty.
4. Vzor Strategy se často používá místo dlouhých řetězců if-elif-else. Jaký je hlavní přínos tohoto
nahrazení?
A) Program spotřebuje méně paměti RAM.
B) Kód je "uzavřený pro změny, ale otevřený pro rozšíření" (Open/Closed principle) – nové chování
přidáme novou třídou, ne úpravou stávající logiky.
C) Python dokáže třídy ve Strategy vzoru vykonávat paralelně.
D) Strategie se v Pythonu používají jen tehdy, když nefunguje dědičnost.
