# Übungen

## Übung 7.1 (✩)

Gegeben ist folgender Code:

```python
x = 42

if x < 0:
    print('negativ')
elif x == 0:
    print('null')
elif x < 10:
    print('einstellig')
elif x < 100:
    print('zweistellig')
else:
    print('dreistellig oder mehr')
```

1. Sagen Sie vorher, welche Ausgabe der Code für `x = 42` erzeugt. Notieren
   Sie Ihre Antwort, bevor Sie den Code ausführen.
2. Führen Sie den Code aus und überprüfen Sie Ihre Vorhersage.
3. Welche Ausgabe ergibt sich für die Werte `-5`, `0`, `7` und `1000`?
   Überlegen Sie zuerst, dann ausführen.
4. Erklären Sie: Warum wird bei `x = 7` nur `"einstellig"` ausgegeben und
   nicht auch `"zweistellig"`? Was wäre passiert, wenn statt elif drei
   unabhängige if-Blöcke verwendet worden wären?

```{code-cell} python
# Code-Zelle
```

## Übung 7.2 (✩)

An einem Druckbehälter wird der Betriebsdruck überwacht. Abhängig vom
gemessenen Druck soll eine der folgenden Meldungen ausgegeben werden:

* Unter 5.0 bar: "Unterdruck: Anlage prüfen."
* 5.0 bar bis unter 10.0 bar: "Normalbetrieb."
* 10.0 bar bis unter 12.0 bar: "Erhöhter Druck: Beobachten."
* Ab 12.0 bar: "Kritisch: Sicherheitsventil öffnen."

Schreiben Sie ein Skript, das nach dem aktuellen Druck in bar fragt und die
entsprechende Meldung ausgibt.

Testen Sie mit den Werten 3.0, 7.5, 11.0 und 13.5 bar.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.3 (✩)

An einer Hochschule gilt folgendes Benotungsschema:

| Punktzahl | Note |
| --------- | ---- |
| 90 bis 100 | 1.0 (sehr gut) |
| 80 bis unter 90 | 2.0 (gut) |
| 70 bis unter 80 | 3.0 (befriedigend) |
| 60 bis unter 70 | 4.0 (ausreichend) |
| unter 60 | 5.0 (nicht bestanden) |

Schreiben Sie ein Skript, das nach der erreichten Punktzahl fragt und die
entsprechende Note ausgibt. Geben Sie dabei sowohl die Note als Zahl als auch
die Bezeichnung aus, zum Beispiel: `"Note: 2.0 (gut)"`.

Testen Sie mit den Werten 95, 83, 72, 65 und 45.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.4 (✩✩)

In einer Produktionsanlage darf eine Maschine nur dann in Betrieb genommen
werden, wenn alle drei folgenden Bedingungen gleichzeitig erfüllt sind:

1. Die Öltemperatur liegt zwischen 40 °C und 80 °C.
2. Der Hydraulikdruck liegt zwischen 3.0 bar und 6.0 bar.
3. Die Drehzahl liegt zwischen 800 U/min und 1500 U/min.

Schreiben Sie ein Skript, das alle drei Werte abfragt. Wenn alle Bedingungen
erfüllt sind, soll ausgegeben werden: `"Freigabe erteilt: Maschine kann
gestartet werden."` Andernfalls: `"Freigabe verweigert: Betriebsparameter
außerhalb des zulässigen Bereichs."`

Testen Sie mit folgenden Wertepaaren:

* (60 °C, 4.5 bar, 1200 U/min) → sollte Freigabe erteilen
* (90 °C, 4.5 bar, 1200 U/min) → sollte Freigabe verweigern
* (60 °C, 4.5 bar, 600 U/min) → sollte Freigabe verweigern

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.5 (✩✩)

Ein Online-Shop bietet kostenlosen Versand unter folgenden Bedingungen an:

* Der Bestellwert beträgt mindestens 50.00 EUR, **oder**
* Der Kunde ist als Premium-Mitglied registriert, **oder**
* Es handelt sich um die erste Bestellung des Kunden.

Schreiben Sie ein Skript, das nach dem Bestellwert in EUR fragt sowie mit
`input()` abfragt, ob der Kunde Premium-Mitglied ist (`"ja"` oder `"nein"`)
und ob es seine erste Bestellung ist (`"ja"` oder `"nein"`). Wenn mindestens
eine der drei Bedingungen erfüllt ist, soll ausgegeben werden:
`"Versandkostenfrei!"`, andernfalls `"Versandkosten: 4.99 EUR"`.

Testen Sie mit folgenden Fällen:

* (30.00 EUR, kein Premium, erste Bestellung) → versandkostenfrei
* (30.00 EUR, kein Premium, nicht erste Bestellung) → Versandkosten
* (75.00 EUR, kein Premium, nicht erste Bestellung) → versandkostenfrei

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.6 (✩✩)

In einem Lottospiel zieht eine Person eine Zufallszahl zwischen 1 und 49.
Gleichzeitig wählt der Spieler seine Glückszahl. Wenn beide Zahlen
übereinstimmen, hat der Spieler gewonnen.

1. Fragen Sie den Benutzer oder die Benutzerin nach seiner oder ihrer
   Glückszahl (ganze Zahl zwischen 1 und 49).
2. Simulieren Sie 10000 Lottoziehungen mit `np.random.randint()`.
3. Zählen Sie, wie viele Ziehungen der Spieler gewonnen hat.
4. Berechnen Sie die Gewinnquote in Prozent.
5. Geben Sie die Ergebnisse mit f-Strings aus:

   ```code
   Glückszahl:     17
   Simulationen:   10000
   Treffer:           19
   Gewinnquote:     0.2 %
   ```

6. Was erwarten Sie theoretisch für die Gewinnquote? Stimmt das simulierte
   Ergebnis damit überein?

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.7 (✩✩✩)

Bei einem Prüfstandstest werden zwei Messsensoren eingesetzt, die unabhängig
voneinander den Zustand einer Maschine als "OK" oder "FEHLER" melden. Wir
modellieren den Ausfall eines Sensors als Zufallsexperiment: Ein Sensor meldet
mit einer Wahrscheinlichkeit von 10 % einen Fehler. Der Fehler wird simuliert,
indem eine Zufallszahl zwischen 1 und 10 erzeugt wird: Zeigt der Würfel eine 1,
meldet der Sensor einen Fehler.

Es gelten folgende Regeln:

* Die Maschine wird abgeschaltet, wenn **beide** Sensoren einen Fehler melden
  (redundantes System: erst wenn beide versagen, wird abgeschaltet).
* Ein Alarm wird ausgelöst, wenn **mindestens ein** Sensor einen Fehler meldet.

Simulieren Sie 5000 Testdurchläufe und ermitteln Sie:

1. Wie viele Durchläufe endeten mit einer Abschaltung (beide Fehler)?
2. Wie viele Durchläufe lösten einen Alarm aus (mindestens ein Fehler)?
3. Wie viele Durchläufe verliefen ohne Ereignis (kein Fehler)?

Geben Sie die absoluten Häufigkeiten und die prozentualen Anteile mit
f-Strings tabellarisch aus und visualisieren Sie die Ergebnisse als
Balkendiagramm.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.8 (✩✩✩)

In Kapitel 5 haben wir Bolzen auf Toleranz geprüft. Jetzt kombinieren wir die
Toleranzprüfung mit einer präziseren Klassifizierung der Ausschussteile.

Ein Bolzen soll einen Durchmesser von 25.0 mm haben, mit einer Toleranz von
±0.3 mm. Bolzen außerhalb der Toleranz werden klassifiziert:

* `d < 24.5 mm`: "grober Unterfehler"
* `24.5 mm ≤ d < 24.7 mm`: "leichter Unterfehler"
* `24.7 mm ≤ d ≤ 25.3 mm`: "iO"
* `25.3 mm < d ≤ 25.5 mm`: "leichter Überfehler"
* `d > 25.5 mm`: "grober Überfehler"

Gegeben sind folgende Messwerte:

```python
durchmesser_mm = [24.3, 24.6, 24.8, 25.0, 25.1, 25.35, 25.6, 24.9, 25.4, 24.4]
```

Schreiben Sie ein Programm, das für jeden Bolzen die Klassifizierung ausgibt
und anschließend die Anzahl in jeder Kategorie zählt und tabellarisch ausgibt.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Übung 7.9 (✩✩✩) Mini-Projekt

In einem Lager werden Pakete automatisch auf ein Förderband sortiert. Jedes
Paket wird nach Gewicht und Abmessungen klassifiziert und einem von drei
Förderbändern zugewiesen:

* **Band 1 (Kleinsendung):** Gewicht unter 2.0 kg **und** kürzeste Seite
  unter 20 cm.
* **Band 2 (Standardpaket):** Gewicht zwischen 2.0 kg und 10.0 kg (jeweils
  einschließlich) **oder** kürzeste Seite zwischen 20 cm und 60 cm (jeweils
  einschließlich).
* **Band 3 (Sperrgut):** Gewicht über 10.0 kg **oder** kürzeste Seite über
  60 cm.

Wenn ein Paket sowohl die Bedingungen für Band 1 als auch für Band 2 erfüllt,
soll es Band 1 zugewiesen werden. Wenn es sowohl Band 2 als auch Band 3
erfüllt, soll es Band 3 zugewiesen werden.

### Teil 1: Einzelpaket

Schreiben Sie ein Skript, das nach Gewicht und kürzester Seite fragt und das
zugehörige Förderband ausgibt.

Testen Sie mit:

* (1.5 kg, 15 cm) → Band 1
* (5.0 kg, 30 cm) → Band 2
* (12.0 kg, 40 cm) → Band 3
* (1.0 kg, 25 cm) → Band 2 (leicht, aber zu groß für Band 1)

### Teil 2: Simulation eines Arbeitstages

Simulieren Sie 200 ankommende Pakete. Erzeugen Sie für jedes Paket zufällige
Werte:

* Gewicht: gleichverteilt zwischen 0.5 kg und 15.0 kg
* kürzeste Seite: gleichverteilt zwischen 5 cm und 80 cm

Zählen Sie, wie viele Pakete auf jedes Band geleitet werden, und visualisieren
Sie das Ergebnis als Balkendiagramm.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```
