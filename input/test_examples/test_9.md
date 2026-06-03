---
source: input/test_examples/test_9.pdf
title: test_9
pages: 1
parsed_at: 2026-06-03T19:44:52.189Z
source_mtime: 2026-06-03T19:27:20.320Z
---

# test_9

## Strana 1

Test 9 – Importy
Jméno a přijímení: ________________________________________
1. Uvažujte soubor skript.py, který obsahuje následující kód. Co se vypíše na standardní výstup, pokud
tento skript spustíme přímo?
```python
def pozdrav ():
    print ( "Ahoj z modulu!" )
    if __name__ == "__main__" :
```
print ( "Skript byl spuštěn přímo." )
```python
else :
```
print ( "Skript byl importován." )
A) Nic se nevypíše. B) Ahoj z modulu! C) Skript byl spuštěn přímo. D) Skript byl importován.
2. Python si ukládá informaci o všech již načtených modulech do speciálního slovníku, aby je nemusel při
každém dalším import načítat znovu z disku.
Otázka: Jak se tento slovník jmenuje a kde ho najdeme?
A) importlib.cache , B) sys.path , C) sys.modules , D) os.environ['PYTHON_MODS']
3. Máme modul data.py , ve kterém je definována hodnota:
# soubor data.py
```python
x = 10
```
V hlavním programu provedeme následující kroky:
```python
import data
from data import x
data.x = 20
x = 30
```
Otázka: Co vypíše příkaz print(data.x, x) na konci programu?
A) 20 30, B) 30 30, C) 20 20, D) 10 10
4. Při použití příkazu import se Python pokusí najít příslušný soubor v seznamu složek, který má uložený v
paměti. Otázka: Ve které proměnné je tento seznam cest (adresářů) uložen?
A) sys.path , B) os.folders , C) importlib.directories , D) python.search_list
test_9.md 2026-05-05
1 / 1
