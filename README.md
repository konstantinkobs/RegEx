# Reguläre Ausdrücke

> Dies sind die Folien und Aufgaben zum Workshop "Reguläre Ausdrücke" vom 8. Oktober 2014 in Geesthacht.

# Links

[Folien](http://konstantinkobs.github.io/RegEx)

[Cheatsheet](http://konstantinkobs.github.io/RegEx/Cheatsheet.pdf)

[Mauerfall Text in regexr.com](http://regexr.com/39l3i)

[Markdown Projekt](http://konstantinkobs.github.io/RegEx/Markdown%20Projekt/markdown.html) (Rechtsklick und *Ziel speichern unter...*)

# Aufgaben

**Hinweis:** Die hier angegebenen Lösungen nicht meistens stark vereinfacht, um einen schnellen Überblick zu bekommen. Um bessere Übereinstimmungen zu bekommen, sollten komplexere Ausdrücke gewählt werden. Die Entscheidung, wie spezifisch der Reguläre Ausdruck sein muss, wird bei der Analyse des Kontextes getroffen.

## Aufgabe 1 *(Telefonnummern)*

Schreiben Sie einen Regulären Ausdruck, der Telefonnummern in einem Text findet.

### Kontext

Gegeben sei eine Mail, in der Telefonnummern stehen. Diese Telefonnummern sollen erkannt werden, sodass man schnell diese Nummern anrufen kann.

Um das ganze so einfach wie möglich zu halten, nehmen wir nur

### Beispiele

```
04152123456
04152 123456
040 789 12 34
0171/123456789
555-45-66-89
```

### Mögliche Lösung

`/\d{3,}([ /-]?\d+)+/g`

## Aufgabe 2 *(Durch 20 teilbar)*

Schreiben Sie einen Regulären Ausdruck, der eine Zahl auf die Teilbarkeit mit 20 prüft.

### Kontext

In einem möglichen Szenario soll ein Nutzer eine Zahl in ein Feld eingeben können. Dann wird angezeigt, ob die angegebene Zahl durch 20 teilbar ist.

Wir beschränken uns nur auf positive Integer-Zahlen.

Außerdem kann die Zahl auch mit führenden Nullen geschrieben werden. `0500` gelte dann als `500`.

### Beispiele

```
Gematcht werden:
0
20
30080
718263781628360

Nicht gematcht:
12
777
0123819230
```

### Mögliche Lösung

Da wir den gesamten String auf die Syntax überprüfen wollen, müssen wir `^` und `$` für den Stringanfang und -ende hinzufügen.

Zum Testen bietet sich das `m`-Flag an.

`/^(\d*[02468])?0$/`

## Aufgabe 3 *(Internet-Adressen)*

Schreiben Sie einen Regulären Ausdruck, der in einem Text Internet-Adressen findet.

### Kontext

In einer Mail oder einer Webseite sollen Links zu Webseiten automatisch gefunden und verlinkt werden.

Es ist sinnvoller, lieber mehr URLs zu matchen als zu wenige. Deshalb sollten wir den Ausdruck relativ allgemein halten.

### Beispiele

```
https://google.de/
http://www.kobs.it/
www.konstantinkobs.de
http://maps.google.de
www.example.com/path/to/some/file.mp3
```

### Mögliche Lösung

`/(https?:\/\/(www\.)?|www\.)[\w\-_\.]+[\/\.\w]*[\/\w]/gi`

### Links

[Vergleich verschiedener Regulärer Ausdrücke, teilweise erhebliche Längenunterschiede](https://mathiasbynens.be/demo/url-regex)

## Aufgabe 4 *(Datumsangaben)*

Schreiben Sie einen Regulären Ausdruck, der alle Datumsangaben im Abschnitt *"Mauerfall"* des deutschen Wikipedia-Artikels *"Berliner Mauer"* findet.

### Kontext

In diesem Wikipedia-Artikel-Abschnitt sind alle Datumsangaben in den Formen `Tag. Monat Jahr`, `Tag. Monat` oder `Monat Jahr` angegeben. Da es sehr unwahrscheinlich ist, dass in Wikipedia logisch falsche Datumsangaben stehen (z.B. `99. Dezember 9999`), können wir hier einen sehr leichten Ansatz wählen.

### Beispiele

```
9. November 1989
10. Oktober 2001
```

### Mögliche Lösung

`/(\d{1,2}\. )?(Januar|Februar|März|April|Mai|Juni|Juli|August|September|Oktober|November|Dezember)( \d{4})?/g`

### Links

[Mauerfall Text in regexr.com](http://regexr.com/39l3i)
[Mauerfall Text bei Wikipedia](http://de.wikipedia.org/wiki/Berliner_Mauer#Mauerfall)

## Aufgabe 5 *(Registrierung mit Mail-Adresse)*

Schreiben Sie einen Regulären Ausdruck, der überprüft, ob eine Mail-Adresse eine gültige Syntax hat.

### Kontext

Bei der Registrierung auf einer Seite mit Email-Adresse sollte halbwegs die Syntax einer angegeben Adresse überprüft werden. Da ein Dienst meistens lieber einen neuen Kunden gewinnt, als ihn dadurch abzuschrecken, dass seine korrekte Mail-Adresse nicht angenommen wird, ist es besser, einen Ausdruck zu schreiben, der lieber mehr als zu wenig Adressen zulässt.

### Beispiele

```
mail@konstantinkobs.de
blablabla@bla-bla.bla.de
```

### Mögliche Lösung

`/^[\w\-+.]+@[\w\-+.]{5,}\.[a-z]{2,}$/i`

### Links

[Ein Link mit einem Regulären Ausdruck, der den offiziellen Standard repräsentiert](http://www.regular-expressions.info/email.html)

## Aufgabe 6 *(IP Adressen)*

Schreiben Sie einen Regulären Ausdruck, der eine IPv4 Adresse auf seine Syntax prüft.

### Kontext

Es soll eine Zeichenkette darauf überprüft werden, ob es sich dabei um eine IPv4 Adresse handelt.

### Beispiele

```
192.168.0.1
8.8.8.8
```

### Mögliche Lösung

`/^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/`

# Lizenz

Die Aufgabenstellungen und Folien stehen unter der [MIT-Lizenz](http://de.wikipedia.org/wiki/MIT-Lizenz) für die Weiterverwendung zur Verfügung.