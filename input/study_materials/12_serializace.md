---
source: input/study_materials/12_serializace.pdf
title: 12_serializace
pages: 32
parsed_at: 2026-06-03T19:25:43.109Z
source_mtime: 2026-06-03T19:24:47.289Z
---

# 12_serializace

## Strana 1

Problém serializace
Václav Alt

## Strana 2

Serializace

## Strana 3

Serializace - Serializační problém
▶ Program pracuje s objekty v paměti.
▶ Někdy je ale potřebujeme:
▶ uložit na disk,
▶ poslat po síti,
▶ uložit do databáze,
▶ předat jinému procesu,
▶ později znovu načíst.
▶ Serializace je převod objektu nebo datové struktury do podoby, kterou lze uložit
nebo přenést.
▶ Deserializace je opačný proces.
objekt v paměti −→ text / bytes −→ soubor / síť / databáze

## Strana 4

Serializace - Proč serializujeme?
▶ Perzistence
▶ výsledek výpočtu chceme zachovat i po ukončení programu
▶ Komunikace
▶ data posíláme přes API, socket, HTTP, message queue
▶ Cache
▶ drahý výpočet provedeme jednou a výsledek uložíme
▶ Reprodukovatelnost
▶ chceme později vědět, jaká data program zpracoval
▶ Ladění a logování
▶ někdy chceme objekt převést do čitelné podoby

## Strana 5

Serializace - Jednoduchý případ: čistá data
1 result = {
2 "molecule": "N2O",
3 "geometry": {
4 "R": 2.3,
5 "theta": 120.0,
6 },
7 "energies": [0.1, 0.2, 0.3],
8 "cross_sections": [1.2, 0.8, 0.5],
9 }
▶ Slovník obsahuje pouze jednoduché typy.
▶ Řetězce, čísla, seznamy, slovníky.
▶ Taková data lze snadno převést například do JSONu.

## Strana 6

Serializace - JSON: textová reprezentace dat
1 import json
2
3 with open ("result.json", "w") as f:
4 json.dump(result, f, indent=2)
5
6 with open ("result.json") as f:
7 loaded = json.load(f)
▶ JSON je čitelný pro člověka.
▶ Je jazykově nezávislý.
▶ Hodí se pro konfigurace, API a jednoduchá data.
▶ Nejde ale o formát pro obecné Python objekty.

## Strana 7

Serializace - JSON není Python
JSON umí reprezentovat jen omezenou sadu typů:
▶ objekt / slovník,
▶ pole / seznam,
▶ řetězec,
▶ číslo,
▶ true , false ,
▶ null .
JSON přímo neumí:
▶ vlastní třídy,
▶ množiny,
▶ funkce,
▶ otevřené soubory,
▶ NumPy pole,
▶ datum a čas bez vlastní konverze,
▶ sdílené reference a cykly.

## Strana 8

Serializace - Kde se objeví problém
1 import json
2
3 class Point:
4 def __init__(self, x, y):
5 self.x = x
6 self.y = y
7
8 p = Point(1.0, 2.0)
9
10 json.dumps(p) # TypeError
▶ JSON neví, co je Point .
▶ Neví, které atributy jsou důležité.
▶ Neví, jak objekt později zrekonstruovat.

## Strana 9

Serializace - Objekt není jen slovník
Objekt může obsahovat:
▶ data,
▶ metody,
▶ identitu,
▶ vazby na jiné objekty,
▶ sdílené reference,
▶ validační pravidla,
▶ cache,
▶ vnější zdroje.
Hlavní problém
Serializace objektu není jen otázka uložení jeho atributů. Musíme rozhodnout, co je
skutečný stav objektu.

## Strana 10

Serializace - Naivní řešení: __dict__
1 class Point:
2 def __init__(self, x, y):
3 self.x = x
4 self.y = y
5
6 p = Point(1.0, 2.0)
7
8 data = p.__dict__
9 print (data)
1 {"x": 1.0, "y": 2.0}
▶ Pro jednoduché objekty to může fungovat.
▶ Je to ale křehké řešení.
▶ Ukládáme implementační detail objektu.

## Strana 11

Serializace - Proč je __dict__ křehké?
▶ Objekt nemusí mít __dict__ .
▶ například třídy používající __slots__
▶ Atributy nemusí odpovídat stabilnímu datovému formátu.
▶ Některé atributy mohou být pouze cache.
▶ Některé atributy mohou být dočasné nebo odvozené.
▶ Přejmenování atributu rozbije stará uložená data.
▶ Obcházíme jasné rozhraní objektu.
Lepší otázka
Jak má vypadat stabilní datová reprezentace objektu?

## Strana 12

Serializace - Dataclass jako strukturovaná data
1 from dataclasses import dataclass, asdict
2
3 @dataclass
4 class Geometry:
5 R: float
6 theta: float
7
8 @dataclass
9 class SimulationResult:
10 molecule: str
11 geometry: Geometry
12 energies: list [ float ]
13 cross_sections: list [ float ]
▶ dataclass je vhodná pro objekty, které hlavně nesou data.
▶ Python za nás vygeneruje běžnou infrastrukturu.
▶ Pořád ale musíme řešit převod do serializovatelné podoby.

## Strana 13

Serializace - Dataclass a převod na slovník
1 result = SimulationResult(
2 molecule="N2O",
3 geometry=Geometry(R=2.3, theta=120.0),
4 energies=[0.1, 0.2, 0.3],
5 cross_sections=[1.2, 0.8, 0.5],
6 )
7
8 data = asdict(result)
1 import json
2
3 with open ("result.json", "w") as f:
4 json.dump(data, f, indent=2)
▶ asdict převede vnořené dataclass objekty na slovníky.
▶ Výsledkem jsou obyčejná data.

## Strana 14

Serializace - Explicitní rekonstrukce objektu
1 with open ("result.json") as f:
2 data = json.load(f)
1 result = SimulationResult(
2 molecule=data["molecule"],
3 geometry=Geometry(**data["geometry"]),
4 energies=data["energies"],
5 cross_sections=data["cross_sections"],
6 )
▶ JSON neobnovuje objekt automaticky.
▶ Vrátí slovníky, seznamy, řetězce a čísla.
▶ Objekt rekonstruujeme explicitně.

## Strana 15

Serializace - Vlastní protokol: to_dict
1 from dataclasses import dataclass
2
3 @dataclass
4 class Geometry:
5 R: float
6 theta: float
7
8 def to_dict(self):
9 return {
10 "R": self.R,
11 "theta": self.theta,
12 }
▶ Objekt sám definuje svou datovou reprezentaci.
▶ Nemusíme ukládat všechny atributy.
▶ Můžeme změnit interní implementaci bez změny formátu.

## Strana 16

Serializace - Vlastní protokol: from_dict
1 @dataclass
2 class Geometry:
3 R: float
4 theta: float
5
6 def to_dict(self):
7 return {"R": self.R, "theta": self.theta}
8
9 @classmethod
10 def from_dict(cls, data):
11 return cls(
12 R=data["R"],
13 theta=data["theta"],
14 )
▶ from_dict je alternativní konstruktor.
▶ Jasně popisuje, jak se objekt obnoví z dat.
▶ Je zde prostor pro validaci a migraci starších verzí.

## Strana 17

Serializace - Vnořené objekty
1 @dataclass
2 class SimulationResult:
3 molecule: str
4 geometry: Geometry
5 energies: list [ float ]
6 cross_sections: list [ float ]
7
8 def to_dict(self):
9 return {
10 "molecule": self.molecule,
11 "geometry":
12 self.geometry.to_dict(),
13 "energies": self.energies,
14 "cross_sections":
15 self.cross_sections,
16 }
1 @classmethod
2 def from_dict(cls, data):
3 return cls(
4 molecule=data["molecule"],
5 geometry=Geometry.from_dict(
6 data["geometry"]
7 ),
8 energies=data["energies"],
9 cross_sections=
10 data["cross_sections"],
11 )
▶ Každá třída odpovídá za převod vlastního stavu.
▶ Složený objekt skládá serializaci z menších částí.

## Strana 18

Serializace - Použití vlastního protokolu
1 result = SimulationResult(
2 molecule="N2O",
3 geometry=Geometry(R=2.3, theta=120.0),
4 energies=[0.1, 0.2, 0.3],
5 cross_sections=[1.2, 0.8, 0.5],
6 )
7
8 with open ("result.json", "w") as f:
9 json.dump(result.to_dict(), f, indent=2)
1 with open ("result.json") as f:
2 loaded = SimulationResult.from_dict(json.load(f))

## Strana 19

Serializace - Výhody explicitního převodu
▶ Formát je čitelný.
▶ Data nejsou závislá na přesné implementaci třídy.
▶ Snadno se testuje.
▶ Snadno se ladí.
▶ Lze přidat validaci.
▶ Lze řešit změny verzí.
▶ Výsledný soubor může použít i jiný program než Python.
Doporučení
Pro dlouhodobě ukládaná data preferujte explicitní datový formát před automatickou
serializací objektů.

## Strana 20

Serializace - Pickle: automatická serializace Python objektů
1 import pickle
2
3 with open ("result.pkl", "wb") as f:
4 pickle.dump(result, f)
5
6 with open ("result.pkl", "rb") as f:
7 loaded = pickle.load(f)
▶ pickle je standardní modul pro serializaci Python objektů.
▶ Umí uložit mnoho objektů bez ručního převodu.
▶ Výsledkem je binární Python-specifický formát.

## Strana 21

Serializace - Kdy se hodí pickle
▶ Rychlá interní cache.
▶ Dočasné uložení mezivýsledku.
▶ Experimentální skripty.
▶ Komunikace mezi Python procesy.
▶ Situace, kdy kontrolujeme zápis i čtení dat.
Typická situace
Výpočet trvá dlouho, data používá jen náš Python program a soubor nebude sloužit
jako veřejný formát.

## Strana 22

Serializace - Problémy s pickle
▶ Není jazykově nezávislý.
▶ Není vhodný jako veřejný datový formát.
▶ Není vhodný pro dlouhodobou archivaci.
▶ Může se rozbít při přejmenování třídy nebo modulu.
▶ Může se rozbít při změně struktury objektu.
▶ Výsledek není dobře čitelný pro člověka.
Důležité
Pickle ukládá Python objekt jako Python objekt. To je pohodlné, ale také křehké.

## Strana 23

Serializace - Bezpečnostní problém pickle
1 with open ("unknown_file.pkl", "rb") as f:
2 obj = pickle.load(f)
Pozor
Nikdy nenačítejte pickle soubor z nedůvěryhodného zdroje.
▶ Deserializace pomocí pickle.load může spustit kód.
▶ Pro data od uživatele, z internetu nebo z veřejného API použijte bezpečnější
formát.
▶ Například JSON neobnovuje libovolné Python objekty.

## Strana 24

Serializace - Čitelnost: JSON vs. pickle
1 import json
2
3 text = json.dumps(
4 result.to_dict(),
5 indent=2,
6 )
7
8 print (text)
▶ textový formát
▶ čitelný
▶ vhodný pro kontrolu
1 import pickle
2
3 binary = pickle.dumps(result)
4
5 print (binary)
▶ binární formát
▶ Python-specifický
▶ nehodí se k ruční editaci

## Strana 25

Serializace - Difficult cases: sdílené reference
▶ V paměti mohou dva objekty odkazovat na stejný objekt.
▶ Při naivním převodu na slovník tuto informaci ztratíme.
a . child −→ x b . child −→ x
Po serializaci může vzniknout:
a . child −→ x 1 b . child −→ x 2
Problém
Jsou x_1 a x_2 dvě kopie, nebo měly být jeden sdílený objekt?

## Strana 26

Serializace - Difficult cases: cykly
1 a.friend = b
2 b.friend = a
▶ Objektový graf může obsahovat cykly.
▶ JSON je stromová struktura.
▶ Strom neumí přímo reprezentovat obecný graf.
Běžné řešení
Objekty se ukládají s identifikátory a odkazy.
1 {"id": 1, "friend_id": 2}
2 {"id": 2, "friend_id": 1}

## Strana 27

Serializace - Difficult cases: vnější zdroje
Některé věci nejsou běžný uložitelný stav:
▶ otevřený soubor,
▶ socket,
▶ databázové spojení,
▶ GUI okno,
▶ vlákno,
▶ lock,
▶ generátor v polovině výpočtu.
Myšlenka
Ukládejte informaci potřebnou k obnovení zdroje, ne samotný živý zdroj.

## Strana 28

Serializace - Difficult cases: změna verze
Dnešní formát:
1 {
2 "name": "Alice"
3 }
Zítřejší formát:
1 {
2 "first_name": "Alice",
3 "last_name": ""
4 }
▶ Dlouhodobě uložená data musí přežít změny programu.
▶ Proto je vhodné ukládat verzi formátu.

## Strana 29

Serializace - Verzování datového formátu
1 {
2 "version": 1,
3 "molecule": "N2O",
4 "geometry": {
5 "R": 2.3,
6 "theta": 120.0
7 },
8 "energies": [0.1, 0.2, 0.3],
9 "cross_sections": [1.2, 0.8, 0.5]
10 }
▶ Čtecí kód může podle verze zvolit správnou interpretaci.
▶ Starší soubory lze migrovat do novější podoby.

## Strana 30

Serializace - Výběr formátu
Situace Vhodné řešení
Konfigurační soubor JSON / TOML / YAML
Jednoduchá tabulková data CSV
Strukturovaná data pro API JSON
Python-only dočasná cache pickle
Dlouhodobá projektová data explicitní schéma + verze
Vlastní třídy to_dict / from_dict
NumPy pole npy / npz
Nedůvěryhodný vstup nikdy pickle
Otázka při návrhu
Kdo bude data číst, kdy, v jakém programu a s jakou verzí kódu?

## Strana 31

Serializace - Shrnutí
▶ Serializace převádí objekt nebo data do uložitelné či přenositelné podoby.
▶ Jednoduchá data se serializují snadno.
▶ Objekty jsou těžší: mají identitu, invarianty, reference a kontext.
▶ JSON je dobrý obecný datový formát, ale nezná Python objekty.
▶ pickle je pohodlný pro Python objekty, ale je nebezpečný pro nedůvěryhodná
data.
▶ Pro dlouhodobá data je lepší navrhnout explicitní formát.
Pravidlo
Serializujte raději data než živé objekty.

## Strana 32

Serializace - Praktické pravidlo na konec
▶ Pokud má soubor přežít refactoring, použijte explicitní formát.
▶ Pokud má soubor číst jiný jazyk, nepoužívejte pickle .
▶ Pokud data pochází z nedůvěryhodného zdroje, nepoužívejte pickle .
▶ Pokud jde o krátkodobou cache ve vlastním Python projektu, pickle může být
rozumný.
▶ Pokud serializujete vlastní třídu, napište jasné to_dict a from_dict .
Nejdřív navrhněte data. Až potom ukládání objektů.
