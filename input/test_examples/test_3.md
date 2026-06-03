---
source: input/test_examples/test_3.pdf
title: test_3
pages: 2
parsed_at: 2026-06-03T19:44:52.152Z
source_mtime: 2026-06-03T19:27:20.353Z
---

# test_3

## Strana 1

test_3.md 2026-03-09
1 / 2
Test 3 – Vícenásobná dědičnost, protokoly
Jméno a přijímení: ________________________________________
1. Je dán následující kód:
```python
class LoggerMixin:
    def save(self, data):
        print(f"[LOG]: Saving data '{data}'")
        super().save(data)

class JsonSaver:
    def save(self, data):
        print(f"Saving as JSON: {data}")

class XmlSaver:
    def save(self, data):
        print(f"Saving as XML: {data}")

class MyDataSaver(LoggerMixin, JsonSaver, XmlSaver):
    pass
saver = MyDataSaver()
saver.save("my_data")
```
Otázka A : Co se vypíše při zavolání saver.save("my_data") ?
A) [LOG]: Saving data 'my_data'
B) Saving as JSON: my_data
C) [LOG]: Saving data 'my_data' následované Saving as JSON: my_data
D) [LOG]: Saving data 'my_data' → Saving as JSON: my_data → Saving as XML: my_data
Otázka B : Proč je použití super() v mixinech vhodné?
A) Aby mixin mohl zavolat metodu v rodičovské třídě a zachoval původní funkčnost.
B) Aby mixin automaticky vytvořil novou instanci rodiče.
C) Aby mixin přepsal všechny metody rodičů a deaktivoval jejich funkčnost.
D) super() není v mixinech doporučené, používá se jen u abstraktních tříd.
2. Jaký je hlavní rozdíl v tom, jak Python kontroluje shodu třídy s protokolem ( typing.Protocol ) oproti
abstraktní třídě ( abc.ABC )?
A) U protokolů musí třída explicitně dědit z daného protokolu v závorkách, jinak ji Python neuzná.

## Strana 2

test_3.md 2026-03-09
2 / 2
B) Protokoly nevyžadují explicitní dědičnost; pokud třída implementuje všechny požadované metody se
správnými signaturami, je považována za kompatibilní.
C) Protokoly fungují pouze za běhu programu (runtime), zatímco ABC kontroluje chyby už při psaní
kódu.
D) Mezi ABC a Protocol není v Pythonu žádný funkční rozdíl, jde pouze o dvě různá pojmenování téhož.
3. Uvažujte následující kód využívající mypy nebo jiný nástroj pro statickou analýzu. Proč by nástroj
nahlásil chybu u volání funkce process_data(my_item) ?
```python
from typing import Protocol

class Drawable(Protocol):
    def draw(self) -> None:
        ...

class Square:
    def draw(self) -> None:
        print("Kreslím čtverec")

class Circle:
    def move(self) -> None:
        print("Posouvám kruh")
def process_data(item: Drawable) -> None:
item.draw()
my_item = Circle()
process_data(my_item)
```
A) Protože třída Circle nedědí explicitně z Drawable (např. class Circle(Drawable): ).
B) Protože process_data vyžaduje objekt typu Drawable , ale Circle neimplementuje metodu
draw() .
C) Protože protokol Drawable obsahuje ... (tři tečky), což je v Pythonu syntaktická chyba.
D) Protože funkce process_data nemá definovanou návratovou hodnotu.
