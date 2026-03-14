# 7.1 Verzweigungen vertiefen: elif und else

In Kapitel 4 haben wir die einfache if-Verzweigung kennengelernt: Wenn eine
Bedingung erfüllt ist, wird ein Code-Block ausgeführt. In Übung 4.6 sind wir
dabei auf ein Problem gestoßen. Bei einer Betriebstemperatur von 95 °C wurden
zwei Meldungen ausgegeben, nämlich "erhöhte Betriebstemperatur" und "kritischer
Bereich", weil zwei unabhängige if-Bedingungen gleichzeitig erfüllt waren. Das
ist korrekt, wenn beide Meldungen gleichzeitig gelten sollen. Oft wollen wir
aber sicherstellen, dass genau eine von mehreren Möglichkeiten ausgewählt wird.
Dafür lernen wir in diesem Kapitel `else` und `elif` kennen.

## Lernziele

* [ ] Sie können mit `if` und `else` eine Verzweigung mit zwei Zweigen
  implementieren.
* [ ] Sie können mit `if`, `elif` und `else` eine Verzweigung mit mehreren
  Zweigen implementieren.
* [ ] Sie wissen, dass bei einem if-elif-else-Konstrukt immer genau ein Zweig
  ausgeführt wird.

## Zwei Zweige: if und else

Bisher konnten wir mit `if` nur entscheiden, ob ein Code-Block ausgeführt wird
oder nicht. Häufig brauchen wir aber zwei klar getrennte Fälle: entweder das
eine oder das andere. Dafür erweitern wir die if-Verzweigung um das Schlüsselwort
`else`.

Kehren wir zum Beispiel der Bremsscheibe aus Kapitel 4 zurück. Diesmal wollen
wir nicht nur eine Warnung ausgeben, wenn die Temperatur zu hoch ist, sondern in
jedem Fall eine Rückmeldung:

```{code-cell} python
# Eingabe
KRITISCHE_TEMPERATUR_C = 300
temperatur_C = 318

# Verarbeitung und Ausgabe
if temperatur_C > KRITISCHE_TEMPERATUR_C:
    print('Warnung: kritische Temperatur überschritten. Bitte anhalten.')
else:
    print('Temperatur im normalen Bereich. Fahrt kann fortgesetzt werden.')
```

Der `else`-Block wird genau dann ausgeführt, wenn die Bedingung des
`if`-Blocks nicht erfüllt ist. Eines der beiden ist immer wahr: Entweder ist
die Temperatur zu hoch, oder sie ist es nicht. Die allgemeine Syntax lautet:

```python
if bedingung:
    anweisungsblock_1   # wird ausgeführt, wenn bedingung True ist
else:
    anweisungsblock_2   # wird ausgeführt, wenn bedingung False ist
```

Nach dem if-else-Konstrukt macht Python mit dem restlichen Code weiter.
Wichtig: `else` hat keine eigene Bedingung. Es ist der "Auffangfall" für
alles, was die if-Bedingung nicht abdeckt.

### Mini-Übung 1

Schreiben Sie ein Skript, das nach der aktuellen Außentemperatur fragt. Wenn
die Temperatur kleiner oder gleich 3 °C ist, soll ausgegeben werden:
"Vorsicht, es besteht Glatteisgefahr!" Andernfalls soll ausgegeben werden:
"Kein Grund zur Sorge."

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Mehrere Zweige: if, elif und else

Zwei Zweige reichen oft nicht aus. In Übung 4.6 hatten wir drei Temperaturbereiche:
Normalbetrieb, erhöhte Temperatur und kritischer Bereich. Mit mehreren
unabhängigen if-Blöcken entstand das Problem, dass für 95 °C zwei Meldungen
ausgegeben wurden.

Eine erste Idee wäre, if-else-Blöcke zu verschachteln:

```{code-cell} python
# Eingabe
temperatur_C = 95.0

# Verschachteltes if-else: unübersichtlich
if temperatur_C < 60:
    print('Normalbetrieb.')
else:
    if temperatur_C < 80:
        print('Erhöhte Betriebstemperatur.')
    else:
        print('Kritischer Bereich.')
```

Das funktioniert korrekt, aber bei vielen Bedingungen wird der Code durch die
Einrückungstiefe schnell unübersichtlich. Python bietet dafür eine elegantere
Lösung: das Schlüsselwort `elif`, das als Kurzform für "else if" steht. Es
ermöglicht mehrere Bedingungen nacheinander zu prüfen, ohne die Einrückungstiefe
zu erhöhen:

```{code-cell} python
# Eingabe
temperatur_C = 95.0

# Übersichtlich mit elif
if temperatur_C < 60:
    print('Normalbetrieb.')
elif temperatur_C < 80:
    print('Erhöhte Betriebstemperatur.')
else:
    print('Kritischer Bereich.')
```

Beide Varianten sind äquivalent, aber die zweite ist deutlich besser lesbar.
Die allgemeine Syntax des if-elif-else-Konstrukts lautet:

```python
if bedingung_1:
    anweisungsblock_1
elif bedingung_2:
    anweisungsblock_2
elif bedingung_3:
    anweisungsblock_3
...
else:
    anweisungsblock_n
```

Das Verhalten ist grundlegend verschieden von mehreren unabhängigen
if-Blöcken: Die Bedingungen werden der Reihe nach geprüft. Sobald eine
Bedingung erfüllt ist, wird der zugehörige Block ausgeführt und alle
nachfolgenden `elif`- und `else`-Zweige werden übersprungen. Bei einem
if-elif-else-Konstrukt wird also immer genau ein Zweig ausgeführt.

Beachten Sie auch die Reihenfolge der Bedingungen: Im obigen Beispiel
prüfen wir zuerst `< 60`, dann `< 80`. Das funktioniert, weil wir im
`elif`-Zweig bereits wissen, dass die erste Bedingung nicht erfüllt war,
also `temperatur_C >= 60` gilt. Der `elif`-Zweig deckt daher den Bereich
60 °C bis unter 80 °C ab.

### Mini-Übung 2

Schreiben Sie ein Skript, das nach der gemessenen Bremsscheibentemperatur fragt
und eine der folgenden Meldungen ausgibt:

* Unter 200 °C: "Normalbetrieb."
* Ab 200 °C bis unter 300 °C: "Erhöhte Temperatur: Fahrstil anpassen."
* Ab 300 °C bis unter 400 °C: "Warnung: Bremsscheibe stark beansprucht."
* Ab 400 °C: "Gefahr: Bremsversagen möglich. Sofort anhalten."

Testen Sie Ihr Skript mit den Temperaturen 150, 250, 350 und 450 °C.
Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

Das if-elif-else-Konstrukt lässt sich auch für beliebig viele Fälle einsetzen.
Die folgende Mini-Übung zeigt ein Beispiel mit zehn Stufen:

### Mini-Übung 3

In Deutschland gilt für Geschwindigkeitsüberschreitungen mit dem PKW innerorts
folgender Bußgeldkatalog (Stand 2021):

| Überschreitung | Bußgeld |
| -------------- | ------- |
| bis 10 km/h | 30 EUR |
| 11 bis 15 km/h | 50 EUR |
| 16 bis 20 km/h | 70 EUR |
| 21 bis 25 km/h | 115 EUR |
| 26 bis 30 km/h | 180 EUR |
| 31 bis 40 km/h | 260 EUR |
| 41 bis 50 km/h | 400 EUR |
| 51 bis 60 km/h | 560 EUR |
| 61 bis 70 km/h | 700 EUR |
| über 70 km/h | 800 EUR |

Schreiben Sie ein Skript, das nach der Geschwindigkeitsüberschreitung in km/h
fragt und das entsprechende Bußgeld ausgibt. Verwenden Sie if-elif-else.

Testen Sie mit den Werten 8, 18, 35 und 75.

```{code-cell} python
# Code-Zelle
```

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir `else` und `elif` kennengelernt. Mit `else` lässt
sich ein zweiter Zweig ergänzen, der ausgeführt wird, wenn die if-Bedingung
nicht erfüllt ist. Mit `elif` können beliebig viele Bedingungen nacheinander
geprüft werden. Bei einem if-elif-else-Konstrukt wird immer genau ein Zweig
ausgeführt: Sobald eine Bedingung zutrifft, werden alle weiteren Zweige
übersprungen. Im nächsten Kapitel erweitern wir die Möglichkeiten der
Verzweigungen um logische Operatoren, mit denen wir mehrere Bedingungen in
einem einzigen Ausdruck kombinieren können.
