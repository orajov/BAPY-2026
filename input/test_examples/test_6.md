---
source: input/test_examples/test_6.pdf
title: test_6
pages: 2
parsed_at: 2026-06-03T19:44:52.174Z
source_mtime: 2026-06-03T19:27:20.346Z
---

# test_6

## Strana 1

test_6.md 2026-03-31
1 / 2
Test 6 – Práce s knihovnou NumPy
Jméno a přijímení: ________________________________________
1. Které z následujících tvrzení nejlépe popisuje hlavní výhodu NumPy polí (ndarray) oproti standardním
Python seznamům?
A) NumPy pole mohou obsahovat různé datové typy v jednom poli (např. string a int zároveň).
B) NumPy automaticky vykresluje grafy při každém výpočtu.
C) NumPy pole jsou optimalizovaná pro matematické operace, jsou výrazně rychlejší a zabírají méně
paměti.
D) V Pythonu nelze provádět násobení čísel bez importu knihovny NumPy.
2. Uvažujte následující kód. Co bude výstupem posledního řádku?
```python
import numpy as np
arr = np.array([1, 2, 3])
result = arr * 2
print(result)
```
A) Dojde k chybě TypeError , protože pole nelze násobit celým číslem.
B) [1, 2, 3, 1, 2, 3]
C) [3, 4, 5]
D) [2, 4, 6]
3. Uvažujte následující kód. Co se vypíše do konzole?
```python
import numpy as np
list_a = [1, 2]
list_b = [3, 4]
array_a = np.array([1, 2])
array_b = np.array([3, 4])
print(list_a + list_b)
print(array_a + array_b)
```
A) [4, 6] [4, 6]
B) [1, 2, 3, 4] [1, 2, 3, 4]

## Strana 2

test_6.md 2026-03-31
2 / 2
C) [1, 2, 3, 4] [4, 6]
D) [4, 6] [1, 2, 3, 4]
4. Co vypíše tento fragment kódu využívající tzv. boolean indexing?
```python
import numpy as np
arr = np.array([10, 20, 30, 40, 50])
mask = arr > 30
print(arr[mask])
```
A) [True, True, True, True, True]
B) [40, 50]
C) [10, 20, 30]
D) 3 (počet prvků větších než 30)
