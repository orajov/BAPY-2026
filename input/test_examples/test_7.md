---
source: input/test_examples/test_7.pdf
title: test_7
pages: 2
parsed_at: 2026-06-03T19:44:52.179Z
source_mtime: 2026-06-03T19:27:20.341Z
---

# test_7

## Strana 1

test_7.md 2026-04-05
1 / 2
Test 7 – Pandas, Matplotlib a Scikit-learn
Jméno a přijímení: ________________________________________
1. Máme DataFrame df , který obsahuje sloupce mesto a populace . Chceme zjistit celkový počet obyvatel
pro každé město zvlášť. Kterou kombinaci metod použijete?
A) df.groupby('mesto')['populace'].sum()
B) df.sort_values('mesto').sum()
C) df.filter('mesto').add('populace')
D) df['mesto'].count()
2. Uvažujte následující fragment kódu. Co se vypíše po jeho spuštění?
```python
import pandas as pd
data = {'vek': [20, 30, 40, 50], 'jmeno': ['Jan', 'Petr', 'Eva', 'Anna']}
df = pd.DataFrame(data)
starsi_nez_35 = df[df['vek'] > 35]
print(len(starsi_nez_35))
```
A) 1, B) 2, C) 3, D) 4
3. Co se stane, pokud spustíte následující kód pro vykreslení grafu?
```python
import matplotlib.pyplot as plt
x = [1, 2, 3]
y = [10, 20, 30]
plt.plot(x, y)
plt.title("Vývoj teploty")
```
# Zde chybí určitý příkaz
A) Graf se automaticky uloží jako soubor chart.png.
B) Graf se vykreslí do konzole jako textová tabulka.
C) Graf se připraví v paměti, ale v mnoha prostředích (např. běžný skript) se nezobrazí okno s grafem,
protože chybí plt.show() .
D) Dojde k chybě, protože seznamy x a y musí být typu numpy.array .

## Strana 2

test_7.md 2026-04-05
2 / 2
4. Který z následujících problémů je typickým příkladem využití lineární regrese?
A) Rozdělení e-mailů do dvou složek: „Spam“ a „Doručená pošta“.
B) Rozpoznávání, zda je na obrázku pes, nebo kočka.
C) Shlukování zákazníků do skupin podle jejich nákupního chování.
D) Předpověď konkrétní ceny nemovitosti (např. 5 420 000 Kč) na základě její rozlohy v m2.
5. Představte si, že zkoumáte závislost výšky rostliny (v cm) na čase (ve dnech). Máte k dispozici následující
kód, který naměřená data proloží lineární regresí. Jaký je význam proměnné trend_y v grafu?
```python
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
import numpy as np
```
# X = dny od zasazení, y = výška v cm
```python
dny = np.array([[1], [3], [7], [10], [14]])
vyska = np.array([2, 5, 12, 18, 24])
model = LinearRegression()
model.fit(dny, vyska)
```
# Výpočet hodnot pro zobrazení spojnice
```python
trend_y = model.predict(dny)
plt.scatter(dny, vyska, color='green', label='Měření')
plt.plot(dny, trend_y, color='black', linestyle='--', label='Trend růstu')
plt.legend()
plt.show()
```
A) Jsou to náhodně vygenerovaná čísla, která slouží pouze k určení délky osy y.
B) Jedná se o seznam chyb (reziduí), tedy rozdílů mezi skutečnou výškou a odhadem modelu.
C) Jsou to výšky rostlin vypočítané modelem pro dané dny, které po vykreslení pomocí plt.plot
vytvoří černou přerušovanou čáru trendu.
D) Tato proměnná obsahuje textové popisky (labely) pro jednotlivé body v grafu.
