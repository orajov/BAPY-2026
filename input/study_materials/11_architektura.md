---
source: input/study_materials/11_architektura.pdf
title: 11_architektura
pages: 63
parsed_at: 2026-06-03T19:25:43.079Z
source_mtime: 2026-06-03T19:24:47.282Z
---

# 11_architektura

## Strana 1

Architektura
Václav Alt

## Strana 2

Motivace

## Strana 3

Motivace - Proč řešit architekturu
1 price = float ( input ("Cena za kus: "))
2 count = int ( input ("čPoet ůkus: "))
3
4 total = price * count
5
6 if total > 10_000:
7 print ("Velká objednávka!")
8
9 print ("Celkem:", total)
▶ Funguje to.
▶ Ale špatně se to testuje, rozšiřuje a znovu používá.
▶ Architektura řeší, kam patří která odpovědnost .

## Strana 4

Motivace - Architektura není jen “velké UML”
▶ Architektura není primárně o třídách.
▶ Je to způsob organizace programu:
▶ co je jádro programu,
▶ co je vstup/výstup,
▶ kdo na kom závisí,
▶ kde vznikají chyby,
▶ co lze nahradit jinou implementací.
▶ I malý skript může mít dobrou nebo špatnou architekturu.

## Strana 5

Motivace - Typické příznaky špatné architektury
▶ Funkce zároveň:
▶ čte vstup,
▶ počítá výsledek,
▶ tiskne výstup,
▶ loguje,
▶ ukončuje program.
▶ Změna formátu výstupu rozbije výpočet.
▶ GUI nelze přidat bez přepsání logiky.
▶ Testy vyžadují simulaci input() a čtení stdout .

## Strana 6

Program jako systém

## Strana 7

Program jako systém - Program jako tok dat
Vstup
↓
Zpracování
↓
Výstup
▶ Vstup: uživatel, soubor, argumenty, síť.
▶ Zpracování: pravidla, výpočty, rozhodování.
▶ Výstup: terminál, GUI, soubor, databáze.

## Strana 8

Program jako systém - Důležitá otázka
Která část programu by měla znát kterou?
▶ Má výpočet vědět, že výstup jde do terminálu?
▶ Má model vědět, že existuje tlačítko v GUI?
▶ Má parsování argumentů znát obchodní pravidla?

## Strana 9

Unix, streamy a rozhraní programu

## Strana 10

Unix, streamy a rozhraní programu - Co je Unix
▶ Historicky operační systém z 70. let.
▶ Dnes také rodina systémů a návrhová tradice:
▶ Linux,
▶ BSD,
▶ macOS,
▶ serverové a cloudové prostředí.
▶ Důležitější než konkrétní systém je styl:
▶ malé nástroje,
▶ textové streamy,
▶ skládání programů.

## Strana 11

Unix, streamy a rozhraní programu - Proč Unix řešíme i na
Windows
▶ Většina serverů, kontejnerů a CI prostředí je Unix-like.
▶ Vývojové nástroje často používají Unixové konvence:
▶ Git,
▶ Python CLI,
▶ Docker,
▶ shell skripty,
▶ build nástroje.
▶ Windows se částečně přibližuje:
▶ PowerShell,
▶ WSL,
▶ terminálové workflow.

## Strana 12

Unix, streamy a rozhraní programu - Standardní streamy
▶ stdin : vstup programu.
▶ stdout : normální datový výstup.
▶ stderr : chyby a diagnostika.
stdin → program → stdout
↘ stderr

## Strana 13

Unix, streamy a rozhraní programu - stdout a stderr
1 import sys
2
3 print ("42") # stdout
4 print ("debug info", file =sys.stderr) # stderr
▶ stdout je výstup pro další program.
▶ stderr je informace pro člověka nebo logovací systém.

## Strana 14

Unix, streamy a rozhraní programu - Přesměrování
1 python app.py > result.txt
2 python app.py 2> errors.txt
3 python app.py > result.txt 2> errors.txt
▶ Data a chyby lze zpracovat odděleně.
▶ To je architektonická hranice na úrovni operačního systému.

## Strana 15

Logging a pozorovatelnost

## Strana 16

Logging a pozorovatelnost - Print není logging
▶ print je dobrý pro výstup programu.
▶ Na diagnostiku je slabý:
▶ nemá úrovně závažnosti,
▶ nejde dobře filtrovat,
▶ často znečistí stdout,
▶ není vhodný pro větší aplikace.

## Strana 17

Logging a pozorovatelnost - Logging
1 import logging
2
3 logger = logging.getLogger(__name__)
4
5 logger.debug("Detail čvýpotu")
6 logger.info("Program ěžbí")
7 logger.warning("řPodezelý vstup")
8 logger.error("čVýpoet selhal")
▶ Logování je průřezová záležitost.
▶ Nemá být hlavní výstup programu.

## Strana 18

Logging a pozorovatelnost - Úrovně logování
▶ DEBUG : detail pro vývojáře.
▶ INFO : běžný průběh programu.
▶ WARNING : nečekaná, ale zvládnutá situace.
▶ ERROR : operace selhala.
▶ CRITICAL : program nemůže pokračovat.

## Strana 19

Separation of concerns

## Strana 20

Separation of concerns - Oddělení odpovědností
▶ Každá část programu má mít jasnou roli.
▶ Typické odpovědnosti:
▶ získání vstupu,
▶ validace,
▶ výpočet,
▶ formátování výstupu,
▶ ukládání dat,
▶ logování.
▶ Čím více rolí má jedna funkce, tím hůř se mění.

## Strana 21

Separation of concerns - Cohesion a coupling
▶ Cohesion :
▶ věci, které patří k sobě, jsou spolu.
▶ modul má jeden jasný účel.
▶ Coupling :
▶ míra závislosti mezi částmi programu.
▶ čím silnější závislost, tím těžší změna.
▶ Cíl:
▶ vysoká cohesion,
▶ nízký coupling.

## Strana 22

Separation of concerns - Směr závislostí
▶ Dobré pravidlo:
▶ vnější vrstvy závisí na vnitřních,
▶ vnitřní vrstvy neznají vnější.
▶ Výpočet nemá znát:
▶ CLI,
▶ GUI,
▶ databázi,
▶ konkrétní souborový formát.

## Strana 23

Vrstvená architektura

## Strana 24

Vrstvená architektura - Vrstvy programu
UI / CLI / API
↓
Application layer
↓
Domain model
↓
Infrastructure
▶ Vrstvy pomáhají držet hranice.
▶ Ne každý program potřebuje všechny vrstvy.

## Strana 25

Vrstvená architektura - Domain model
▶ Jádro programu.
▶ Obsahuje:
▶ datové struktury,
▶ výpočty,
▶ pravidla,
▶ validaci významu.
▶ Nemá obsahovat:
▶ input() ,
▶ print() ,
▶ GUI widgety,
▶ parsování CLI argumentů.

## Strana 26

Vrstvená architektura - Application layer
▶ Řídí konkrétní use-case.
▶ Odpovídá na otázku:
▶ co se má stát, když uživatel spustí příkaz?
▶ Typicky:
▶ zavolá model,
▶ rozhodne, co udělat s výsledkem,
▶ zachytí očekávané chyby,
▶ předá data view vrstvě.

## Strana 27

Vrstvená architektura - Infrastructure
▶ Technické detaily:
▶ soubory,
▶ databáze,
▶ síť,
▶ externí knihovny,
▶ konfigurace prostředí.
▶ Infrastructure je často nejméně stabilní část.
▶ Proto by na ní nemělo záviset jádro aplikace.

## Strana 28

MVC

## Strana 29

MVC - Model-View-Controller
▶ Model
▶ data a pravidla programu.
▶ View
▶ prezentace výsledků.
▶ Controller
▶ přijímá vstup a volá správné operace.
Controller → Model → View

## Strana 30

MVC - MVC není jen GUI pattern
▶ V GUI:
▶ View = okna, tlačítka, formuláře.
▶ Controller = callbacky.
▶ V CLI:
▶ View = textový výstup.
▶ Controller = parsování argumentů a běh příkazu.
▶ Ve webu:
▶ View = HTML/JSON.
▶ Controller = endpoint.

## Strana 31

Ports and adapters

## Strana 32

Ports and adapters - Ports and adapters
▶ Také známé jako hexagonální architektura.
▶ Jádro aplikace komunikuje přes rozhraní.
▶ Konkrétní technologie jsou adaptéry:
▶ CLI adaptér,
▶ GUI adaptér,
▶ databázový adaptér,
▶ souborový adaptér.

## Strana 33

Ports and adapters - Proč je to užitečné
▶ Stejný model lze použít ve více prostředích.
▶ Lze vyměnit technickou implementaci:
▶ soubor místo databáze,
▶ CLI místo GUI,
▶ testovací fake místo reálné služby.
▶ Jádro programu zůstává stabilní.

## Strana 34

Dependency injection

## Strana 35

Dependency injection - Dependency injection
▶ Funkce nebo objekt nedostává závislosti “natvrdo”.
▶ Závislost mu předáme zvenku.
▶ Výhody:
▶ snadnější testování,
▶ menší coupling,
▶ možnost výměny implementace.

## Strana 36

Dependency injection - Bez dependency injection
1 def save_report(text):
2 with open ("report.txt", "w") as f:
3 f.write(text)
▶ Funkce pevně závisí na konkrétním souboru.
▶ Test musí pracovat se souborovým systémem.

## Strana 37

Dependency injection - S dependency injection
1 def save_report(text, output):
2 output.write(text)
▶ Funkci nezajímá, kam se zapisuje.
▶ Může to být soubor, StringIO , socket, buffer.

## Strana 38

Chyby a konfigurace

## Strana 39

Chyby a konfigurace - Error handling jako architektonická otázka
▶ Kde chyba vzniká?
▶ Kde se má zachytit?
▶ Co má vidět uživatel?
▶ Co má být v logu?
▶ Model může vyhodit výjimku.
▶ Controller rozhodne, jak ji prezentovat.
▶ View vytvoří text chyby.

## Strana 40

Chyby a konfigurace - Špatně: ukončení programu v modelu
1 def compute_total(price, count):
2 if price < 0:
3 print ("Chyba")
4 exit(1)
5
6 return price * count
▶ Model rozhoduje o UI i ukončení programu.
▶ Nelze ho rozumně použít v GUI nebo testech.

## Strana 41

Chyby a konfigurace - Lépe: výjimka v modelu
1 def compute_total(price, count):
2 if price < 0:
3 raise ValueError("Cena nesmí být záporná")
4
5 return price * count
▶ Model hlásí problém.
▶ Controller rozhodne, co s ním.

## Strana 42

Chyby a konfigurace - Konfigurace
▶ Konfigurace nemá být rozházená v kódu.
▶ Typické zdroje:
▶ argumenty příkazové řádky,
▶ konfigurační soubor,
▶ proměnné prostředí,
▶ defaultní hodnoty.
▶ Konfigurace je vstup aplikace, ne business logika.

## Strana 43

Event-driven architektura

## Strana 44

Event-driven architektura - Event-driven program
▶ Program neběží jen lineárně shora dolů.
▶ Čeká na události:
▶ kliknutí,
▶ změna vstupu,
▶ timer,
▶ zpráva ze sítě.
▶ Události obsluhují handlery.

## Strana 45

Event-driven architektura - Event loop
čekej na událost
↓
najdi handler
↓
zavolej handler
↓
aktualizuj stav / view
▶ GUI frameworky tento loop obvykle skrývají.
▶ Architektonicky je důležité, co handler dělá.

## Strana 46

Event-driven architektura - Handler nemá být celý program
▶ Špatný callback:
▶ čte hodnoty z widgetů,
▶ validuje,
▶ počítá,
▶ formátuje,
▶ ukládá,
▶ loguje.
▶ Lepší callback:
▶ převezme vstup,
▶ zavolá application layer,
▶ aktualizuje view.

## Strana 47

Ukázkový refaktoring

## Strana 48

Ukázkový refaktoring - Start: monolitický skript
1 print ("Kalkulacka objednavky")
2
3 price = float ( input ("Cena za kus: "))
4 count = int ( input ("Pocet kusu: "))
5 discount = float ( input ("Sleva v %: ") or "0")
6
7 total = price * count
8 total -= total * discount / 100
9
10 if total > 10_000:
11 print ("Velka objednavka!")
12
13 print (f"Celkem: {total:.2f} Kc")

## Strana 49

Ukázkový refaktoring - Co je v jednom skriptu smíchané
▶ UI texty.
▶ Parsování vstupu.
▶ Business pravidla.
▶ Výpočet.
▶ Diagnostika.
▶ Formátování výstupu.

## Strana 50

Ukázkový refaktoring - Model: čistá logika
1 def compute_total(price, count, discount=0.0):
2 if price < 0:
3 raise ValueError("Cena nesmi být zaporna")
4 if count < 0:
5 raise ValueError("Pocet nesmi byt zaporny")
6 if not 0 <= discount <= 100:
7 raise ValueError("Sleva musi byt 0 ža 100")
8
9 subtotal = price * count
10 return subtotal - subtotal * discount / 100

## Strana 51

Ukázkový refaktoring - View: formátování
1 def format_total(total):
2 return f"Celkem: {total:.2f} Kc"
3
4
5 def format_error(error):
6 return f"Chyba: {error}"
▶ View nepočítá.
▶ Pouze rozhoduje, jak výsledek vypadá.

## Strana 52

Ukázkový refaktoring - Controller: tok programu
1 import sys
2
3 def run_cli():
4 try :
5 price = float ( input ("Cena za kus: "))
6 count = int ( input ("čPoet ůkus: "))
7 discount = float ( input ("Sleva v %: ") or "0")
8
9 total = compute_total(price, count, discount)
10 print (format_total(total))
11
12 except ValueError as e:
13 print (format_error(e), file =sys.stderr)

## Strana 53

Ukázkový refaktoring - Interpretace
▶ compute_total
▶ model / domain logic.
▶ format_total
▶ view.
▶ run_cli
▶ controller / application flow.
▶ stderr
▶ diagnostický výstup.

## Strana 54

Ukázkový refaktoring - Stejný model, jiné rozhraní
1 def on_button_clicked():
2 price = float (price_input.get())
3 count = int (count_input.get())
4 discount = float (discount_input.get() or "0")
5
6 total = compute_total(price, count, discount)
7
8 result_label.set_text(format_total(total))
▶ Model se nemění.
▶ Mění se pouze adaptér: CLI nebo GUI.

## Strana 55

Moduly a struktura projektu

## Strana 56

Moduly a struktura projektu - Jednoduchá struktura
1 order_app/￿￿￿
2 model.py￿￿￿
3 view.py￿￿￿
4 controller.py￿￿￿
5 main.py
▶ model.py : výpočty a pravidla.
▶ view.py : formátování výstupu.
▶ controller.py : průběh programu.
▶ main.py : vstupní bod.

## Strana 57

Moduly a struktura projektu - Kdy strukturu nezvětšovat
▶ Není potřeba dělat framework z každého skriptu.
▶ Varovné signály, že struktura začíná dávat smysl:
▶ přibývá více způsobů vstupu,
▶ přibývá více výstupních formátů,
▶ výpočet má pravidla a výjimky,
▶ chcete psát testy,
▶ část kódu chcete použít jinde.

## Strana 58

Testovatelnost

## Strana 59

Testovatelnost - Test čisté funkce
1 def test_compute_total_with_discount():
2 total = compute_total(100, 3, discount=10)
3 assert total == 270
▶ Test neřeší input() .
▶ Test nečte stdout .
▶ Testuje přesně jednu věc.

## Strana 60

Testovatelnost - Architektura a testy
▶ Dobře oddělený model se testuje snadno.
▶ Controller se testuje hůř, protože koordinuje I/O.
▶ View lze testovat jako formátování.
▶ Infrastructure lze nahradit fake objekty.

## Strana 61

Praktická pravidla

## Strana 62

Praktická pravidla - Pravidla pro menší Python programy
▶ Výpočet nemá volat input() ani print() .
▶ Chyby z modelu hlaste výjimkami.
▶ Výstup programu posílejte na stdout .
▶ Diagnostiku posílejte na stderr nebo logging.
▶ Konfiguraci předávejte dovnitř, neschovávejte ji globálně.

## Strana 63

Praktická pravidla - Co si odnést
▶ Architektura je o hranicích.
▶ MVC je jen jeden způsob pojmenování rolí.
▶ Důležitější principy:
▶ oddělení odpovědností,
▶ směr závislostí,
▶ nízký coupling,
▶ testovatelná logika,
▶ vyměnitelné adaptéry.
