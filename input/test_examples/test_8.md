---
source: input/test_examples/test_8.pdf
title: test_8
pages: 1
parsed_at: 2026-06-03T19:44:52.184Z
source_mtime: 2026-06-03T19:27:20.323Z
---

# test_8

## Strana 1

Test 8 – Pandas, Matplotlib a SQL
Jméno a přijímení: ________________________________________
1. Máme SQL tabulku produkty . Který SQL dotaz vybere názvy všech produktů (sloupec nazev ), jejichž
cena je vyšší než 1000?
A) SELECT * WHERE cena > 1000
B) SELECT nazev FROM produkty WHERE cena > 1000
C) df.query('cena > 1000')
D) SELECT cena FROM produkty HAVING nazev > 1000
2. Prohlédněte si následující kód v Pythonu. Co bude výsledkem print(len(df_vysledek)) ?
```python
import pandas as pd
import sqlite3
```
# Připojení k databázi na disku
```python
conn = sqlite3.connect( 'databaze.db' )
```
# Příprava dat a uložení do tabulky
```python
data = { 'id' : [ 1 , 2 , 3 ], 'polozka' : [ 'A' , 'B' , 'C' ]}
df = pd.DataFrame(data)
df.to_sql( 'sklad' , conn, if_exists= 'replace' , index= False )
# Dotaz na data
query = "SELECT * FROM sklad WHERE id < 3"
df_vysledek = pd.read_sql_query(query, conn)
print ( len (df_vysledek))
conn.close()
```
A) 1, B) 2, C) 3, D) Kód skončí chybou.
3. Chceme v Matplotlib vykreslit sloupcový graf (bar chart). Kterou funkci k tomu použijete?
A) plt.plot() , B) plt.scatter() , C) plt.bar() , D) plt.histogram()
4. Chceme v SQL spojit data ze dvou tabulek (např. zakaznici a objednavky ) do jednoho celku na
základě společného ID. Které klíčové slovo k tomu v SQL příkazu použijete?
A) GROUP BY , B) WHERE , C) JOIN , D) CONNECT
test_8.md 2026-04-13
1 / 1
