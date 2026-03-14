# 7.2 Logische Operatoren und Simulation

In Kapitel 7.1 haben wir gelernt, wie wir mit if-elif-else zwischen mehreren
Fällen unterscheiden. Oft reicht eine einzelne Bedingung aber nicht aus: Eine
Maschine soll nur dann starten, wenn der Sicherheitsschalter aktiviert ist
**und** die Temperatur im zulässigen Bereich liegt. Ein Alarm soll ausgelöst
werden, wenn der Druck zu hoch ist **oder** die Temperatur einen Grenzwert
überschreitet. Für solche Anforderungen gibt es in Python die **logischen
Operatoren** `and` und `or`. In der zweiten Hälfte dieses Kapitels wenden wir
sie direkt in einer Simulation an: Mit `np.random.randint()` simulieren wir
Würfelwürfe und prüfen kombinierte Gewinnbedingungen.

## Lernziele

* [ ] Sie können mit `and` zwei Bedingungen so verknüpfen, dass beide erfüllt
  sein müssen.
* [ ] Sie können mit `or` zwei Bedingungen so verknüpfen, dass mindestens eine
  erfüllt sein muss.
* [ ] Sie können mit `not` eine Bedingung umkehren.
* [ ] Sie können mit `np.random.randint()` ganzzahlige Zufallszahlen erzeugen.
* [ ] Sie können logische Operatoren in einer Simulation einsetzen, um
  kombinierte Bedingungen zu prüfen.

## Das logische UND: and

Beim logischen `and` müssen beide Bedingungen erfüllt sein, damit der gesamte
Ausdruck `True` ergibt. Das entspricht einer Reihenschaltung in der
Elektrotechnik: Nur wenn beide Schalter geschlossen sind, fließt Strom.

Die Wahrheitstabelle für `and`:

| Bedingung 1 | Bedingung 2 | Ergebnis |
| ----------- | ----------- | -------- |
| `True` | `True` | `True` |
| `True` | `False` | `False` |
| `False` | `True` | `False` |
| `False` | `False` | `False` |

Ein automatisches Werkzeug darf nur dann betätigt werden, wenn das Werkstück
korrekt eingespannt ist **und** der Sicherheitsbereich frei ist:

```{code-cell} python
# Eingabe
werkstueck_eingespannt = True
sicherheitsbereich_frei = False

# Verarbeitung und Ausgabe
if werkstueck_eingespannt and sicherheitsbereich_frei:
    print('Werkzeug kann betätigt werden.')
else:
    print('Sicherheitsvoraussetzungen nicht erfüllt.')
```

Klammern verbessern bei komplexeren Bedingungen die Lesbarkeit, auch wenn sie
syntaktisch nicht immer erforderlich sind:

```{code-cell} python
# Eingabe
temperatur_C = 75.0
druck_bar = 3.5

# Verarbeitung und Ausgabe
if (temperatur_C < 80) and (druck_bar < 4.0):
    print('System arbeitet im normalen Betriebsbereich.')
else:
    print('System außerhalb der normalen Parameter.')
```

Python erlaubt auch verkettete Vergleiche, die gut lesbar sind:

```{code-cell} python
# Eingabe
temperatur_C = 75.0

# Verarbeitung und Ausgabe
if 60 <= temperatur_C <= 85:
    print('Temperatur im zulässigen Betriebsbereich.')
```

Der Ausdruck `60 <= temperatur_C <= 85` ist eine Kurzform für
`(temperatur_C >= 60) and (temperatur_C <= 85)` und entspricht der
mathematischen Schreibweise für Intervalle.

### Mini-Übung 1

Eine Hydraulikpresse darf nur betätigt werden, wenn

1. die Betriebstemperatur zwischen 60 °C und 85 °C liegt und
2. der Druck zwischen 2.5 bar und 5.0 bar liegt.

Schreiben Sie ein Skript, das beide Werte abfragt und eine entsprechende
Meldung ausgibt. Testen Sie mit den Werten (70 °C, 3.5 bar) und (90 °C,
3.5 bar).

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Das logische ODER: or

Beim logischen `or` genügt es, wenn mindestens eine der Bedingungen erfüllt
ist. Das entspricht einer Parallelschaltung in der Elektrotechnik: Es reicht,
wenn einer der beiden Schalter geschlossen ist.

Die Wahrheitstabelle für `or`:

| Bedingung 1 | Bedingung 2 | Ergebnis |
| ----------- | ----------- | -------- |
| `True` | `True` | `True` |
| `True` | `False` | `True` |
| `False` | `True` | `True` |
| `False` | `False` | `False` |

Ein Notabschaltsystem muss aktiviert werden, wenn entweder die Temperatur zu
hoch ist **oder** der Druck einen kritischen Wert überschreitet:

```{code-cell} python
# Eingabe
temperatur_C = 95.0
druck_bar = 4.8

# Verarbeitung und Ausgabe
if (temperatur_C > 90) or (druck_bar > 5.0):
    print('WARNUNG: Notabschaltung wird eingeleitet!')
else:
    print('System arbeitet im normalen Betriebsbereich.')
```

Hier ist die Temperatur mit 95 °C bereits über dem Grenzwert. Der gesamte
Ausdruck ist daher `True`, auch wenn der Druck mit 4.8 bar noch im
zulässigen Bereich liegt.

### Mini-Übung 2

Schreiben Sie ein Programm für das Alarmsystem einer CNC-Fräse. Ein Alarm soll
ausgelöst werden, wenn mindestens eine der folgenden Bedingungen erfüllt ist:

1. Die Drehzahl fällt unter 500 U/min oder steigt über 2000 U/min.
2. Die Kühlmitteltemperatur steigt über 60 °C.

Lassen Sie die Werte eingeben und geben Sie eine entsprechende Meldung aus.
Testen Sie mit (1200 U/min, 55 °C) und (2500 U/min, 55 °C).

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Das logische NICHT: not

Der Operator `not` kehrt einen Wahrheitswert um: aus `True` wird `False` und
umgekehrt. Er wird verwendet, wenn es natürlicher ist, eine Bedingung zu
verneinen:

```{code-cell} python
# Eingabe
wartungsmodus_aktiv = True

# Verarbeitung und Ausgabe
if not wartungsmodus_aktiv:
    print('Maschine kann gestartet werden.')
else:
    print('Maschine im Wartungsmodus: Start nicht möglich.')
```

`not` wird in der Praxis seltener benötigt als `and` und `or`, ist aber
manchmal nützlich, um Bedingungen klarer zu formulieren.

## Ganzzahlige Zufallszahlen: np.random.randint()

In Kapitel 6.2 haben wir `np.random.uniform()` und `np.random.normal()` für
kontinuierliche Zufallszahlen kennengelernt. Für diskrete Situationen, also
wenn nur bestimmte ganzzahlige Werte möglich sind, verwenden wir
`np.random.randint(low, high)`. Diese Funktion erzeugt eine zufällige ganze
Zahl, die größer oder gleich `low` und kleiner als `high` ist.

Für einen klassischen sechsseitigen Würfel, der die Augenzahlen 1 bis 6
liefert, schreiben wir:

```{code-cell} python
import numpy as np

# Einen Würfelwurf simulieren
augenzahl = np.random.randint(1, 7)   # 1 bis 6, da 7 ausgeschlossen ist
print(f"Gewürfelte Augenzahl: {augenzahl}")
```

Beachten Sie: Die obere Grenze `high` ist immer ausgeschlossen. Für Augenzahlen
von 1 bis 6 muss daher `high = 7` angegeben werden.

### Mini-Übung 3

Erzeugen Sie eine Zufallszahl für einen zwanzigseitigen Würfel (W20), wie er
in Rollenspielen verwendet wird. Dieser liefert Augenzahlen von 1 bis 20.
Geben Sie die gewürfelte Zahl mit einem f-String aus:
`"W20-Wurf: 14"`

```{code-cell} python
# Code-Zelle
```

## Simulation mit kombinierten Bedingungen

Jetzt verbinden wir `np.random.randint()` mit den logischen Operatoren. Wir
simulieren ein einfaches Würfelspiel mit zwei Würfeln.

**Die Regeln:** Zwei Würfel werden geworfen. Der Spieler gewinnt, wenn die
Augensumme mindestens 9 beträgt **und** beide Würfel verschiedene Augenzahlen
zeigen. Bei einem Pasch (beide Würfel gleich) zählt der Wurf als verloren,
egal wie hoch die Summe ist.

```{code-cell} python
import numpy as np
import plotly.express as px

# Eingabe
ANZAHL_WUERFE = 1000

# Verarbeitung
anzahl_gewonnen = 0
anzahl_verloren = 0

for i in range(ANZAHL_WUERFE):
    wuerfel_1 = np.random.randint(1, 7)
    wuerfel_2 = np.random.randint(1, 7)
    augensumme = wuerfel_1 + wuerfel_2

    # Gewinnbedingung: Summe >= 9 UND kein Pasch
    if (augensumme >= 9) and (wuerfel_1 != wuerfel_2):
        anzahl_gewonnen = anzahl_gewonnen + 1
    else:
        anzahl_verloren = anzahl_verloren + 1

gewinnquote = anzahl_gewonnen / ANZAHL_WUERFE * 100

# Ausgabe
print(f"Gewonnen:     {anzahl_gewonnen:4d} von {ANZAHL_WUERFE}")
print(f"Verloren:     {anzahl_verloren:4d} von {ANZAHL_WUERFE}")
print(f"Gewinnquote:  {gewinnquote:.1f} %")

fig = px.bar(x=["Gewonnen", "Verloren"],
             y=[anzahl_gewonnen, anzahl_verloren],
             labels={"x": "Ergebnis", "y": "Anzahl"},
             title=f"Würfelspiel: Simulation von {ANZAHL_WUERFE} Runden")
fig.show()
```

Bei 1000 simulierten Runden sollte die Gewinnquote ungefähr bei 22 % liegen.
Durch den Zufall schwankt das Ergebnis von Ausführung zu Ausführung leicht.

### Mini-Übung 4

Verändern Sie die Gewinnbedingung: Der Spieler soll gewinnen, wenn mindestens
einer der beiden Würfel eine 6 zeigt **oder** die Augensumme genau 7 beträgt.

Passen Sie den Code an, führen Sie die Simulation aus und beobachten Sie, wie
sich die Gewinnquote verändert. Ist die neue Gewinnquote höher oder niedriger
als beim ursprünglichen Spiel? Warum?

Strukturieren Sie Ihren Code mit EVA-Kommentaren.

```{code-cell} python
# Code-Zelle
```

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir die logischen Operatoren `and`, `or` und `not`
kennengelernt. Mit `and` müssen beide Teilbedingungen wahr sein, mit `or` genügt
eine. Diese Operatoren ermöglichen es, präzise und realistische Bedingungen zu
formulieren, wie sie in technischen Steuerungen und Simulationen täglich
vorkommen. Kombiniert mit `np.random.randint()` können wir diskrete Prozesse
wie Würfelwürfe simulieren und Gewinnwahrscheinlichkeiten berechnen. Im nächsten
Kapitel lernen wir, eigene Funktionen zu schreiben, mit denen wir häufig
verwendeten Code bündeln und wiederverwenden können.
