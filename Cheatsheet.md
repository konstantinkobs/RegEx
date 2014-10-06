# Informationen

Alle Materialien sind unter `http://github.com/konstantinkobs/RegEx/` abrufbar.

# Cheatsheet

## Aufbau
```
/Pattern/Flags
```

- Die `/` vor und nach dem `Pattern` heißen **Delimiter/Begrenzer**
- `Pattern` beschreibt den Aufbau der zu suchenden Zeichenkette
- `Flags` sind optional und beeinflussen die Art und Weise, wie im Text nach dem Pattern gesucht wird

## Pattern

Bis auf einige Zeichen mit besonderer Bedeutung (**Metacharacters**) stehen alle Zeichen im Pattern für sich selbst. Um *Metacharacters* für sich selbst stehen zu lassen, müssen sie mit einem Backslash (`\`) davor escaped werden.

- `|` ist der `Oder`-Operator, d.h. was links oder rechts steht muss zutreffen
- `( )` definieren Gruppen
- `{min,max}` hinter einem Buchstaben oder einer Gruppe geben die minimale und maximale Wiederholungsanzahl an; `{min,}` matcht alles **ab** `min` Vorkommnissen; `{anzahl}` matcht die genaue Anzahl `anzahl`
- *Quantoren:* `+ = {1,}`, `* = {0,}` und `? = {0,1}`
- `[ ]` wählen ein Zeichen aus der Menge der darin stehenden Zeichen aus
- `[a-z]` matcht einen lateinischen Kleinbuchstaben, `[A-F]` einen lateinischen Großbuchstaben von A bis F
- `.` matcht jedes Zeichen *(bis auf neue Zeilen)*
- `[^a]` bedeutet: Jedes Zeichen außer `a`
- `^` und `$` bezeichnen den Anfang und das Ende des zu durchsuchenden Textes
- `\d = [0-9]`; `\D = [^\d]`
- `\w = [a-zA-Z0-9]`; `\W = [^\w]`
- `\s` sind Leerräume und neue Zeilen; `\S` Gegenteil
- `\b` stellt Wortanfänge und -enden dar

## Flags

Flags sind Buchstaben, die am Ende des Regulären Ausdruckes stehen. Sie haben keine zu beachtende Reihenfolge und sind komplett optional. Ein Regulärer Ausdruck kann also auch nur aus den Delimitern und dem Pattern bestehen.

Folgende drei Flags sind die bekanntesten:

- `g` *(__g__lobal)*: Sucht alle Vorkommnisse im Text
- `i` *(__i__gnore case)*: Nicht mehr auf Groß- und Kleinschreibung achten
- `m` *(__m__ultiline)*: `^` und `$` beziehen sich nicht auf den Anfang und das Ende des *Strings*, sondern jeder *Zeile*.

## Greedy und Lazy *(Gierig und Genügsam)*

Reguläre Ausdrücke sind von Haus aus *greedy*, das heißt, es wird eine möglichst große Zeichenkette gematcht. Manchmal ist dies nicht das gewünschte Verhalten. Der `+`-Quantor lässt sich mit einem nachgestellten `?` *lazy* machen, sprich, er matcht so kurze Zeichenketten wie möglich.

## Backreference

Ein Pattern matcht einen Teil oder die gesamte Zeichenkette. Manchmal möchte man aber nicht alles aus diesem Match weiter verwenden, sondern nur Teile davon. **Beispiel:** Im Text ist der Inhalt, den wir extrahieren wollen, auf beiden Seiten mit `===` eingeschlossen. Der Reguläre Ausdruck `/===.+?===/g` würde alle Vorkommnisse finden, allerdings würden dort auch immer die `===` auf beiden Seiten mit vorkommen.

**Lösung:** Nutzen wir *Gruppen*, also schließen wir Teile des Ausdrucks in Klammern ein, so können wir auf diese Gruppen später zugreifen. Der Ausdruck `/===(.+?)===/g` findet immer noch alle Vorkommnisse, allerdings wird auch der Inhalt in den Klammern nochmals einzeln gespeichert. Man kann dann auf die Inhalte der Gruppen im selben Ausdruck mit `\1` für die erste Gruppe, `\2` für die zweite Gruppe usw. zurückreferenzieren. Beim Ersetzen mit Hilfe von Regulären Ausdrucken wird üblicherweise mit `$1` auf die erste Gruppe zugegriffen.